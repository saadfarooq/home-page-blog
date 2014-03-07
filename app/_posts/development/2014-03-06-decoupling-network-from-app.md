---
layout: post
title: Decoupling Your Network From Your Android App
---

I recently changed from [`HttpUrlConnection`](http://developer.android.com/reference/java/net/HttpURLConnection.html) to the [`Volley`](https://developers.google.com/events/io/sessions/325304728) library for Android networking. Since the time that I wrote that first implementation, I've learned a thing or two about testing and writing clean code. One of the principles that I live by is:
    
    One object should only do one thing

What this means is that any class should have one objective and it should be good at that and not worry about doing other stuff. Any information that the object needs should be passed into it (preferably through some form of `dependency injection`).

## Naive Implementation

So bringing that into the context of an Android `Activity`, the following is an example of a naive implementation that gets data from a webservice.

    public class MyActivity extends Activity implements AsyncCallBack {
    	@Override
		public void onCreate(Bundle savedInstanceState) {
			new AsyncJsonGetTask(this).execute(Service.GET_APPLES);
		}
        @Override
        public void onBackgroundTaskComplete(Object result) {
            Apple[] apples = (Apple[]) result;
            // do something with apples
        }
    }

This was my first implementation. Not so bad I guess. I had an `AsyncTask` subclass that takes care of all of the network stuff in the background, then calls the calling activity via the `AsyncCallBack` interface that includes the `onBackgroundTaskCompleted` method. The actual network library used was figured out by another class. There are obvious drawbacks to this, such as the casting which did cause some issues in case of errors and also that it's not easy to test.

## Migrating to Volley
Then [`Volley`](https://developers.google.com/events/io/sessions/325304728) came out and I had planned to move to [`Dagger`](http://square.github.io/dagger/) for dependency injection so my implementation became:

    public class MyActivity extends Activity implements AsyncCallback {
        @Inject RequestQueue mRequestQueue;
        @Inject ApplesRequest mRequest;

        @Override
        public void onCreate(Bundle savedInstanceState) {
            mRequest.setCaller(this);
            mRequest.setMaxApples(20);
            mRequestQueue.add(mRequest);
        }

        @Override
        public void onBackgroundTaskComplete(Object result) {
            Apple[] apples = (Apple[]) result;
            // do something with apples
        }

        @Override
        public void onStop() {
            mRequestQueue.cancelAll(); // Cancel any pending requests when activity stops
        }
    }

This time I use dependency injection. I use a subclass of the Volley `Request` object that is related to one particular service. This removes some of the generics but because of the way callbacks are configured, the casting is still there. However, this can be easily fixed by having different interfaces associated with different `Request` objects.
Testing of course, is much easier now. You inject a mock `RequestQueue` for the test and it simply calls back with mock data instead of calling the actual service.

*Note*: I also switched to [`EventBus`](https://github.com/greenrobot/EventBus) to make avoid having to many callback interfaces both in these cases and Fragment-Activity communication.

So it seems problem solved. But the implementation is still tightly coupled. If I were to move to some new library from Volley, there would be a lot of refactoring. Not good.

## Complete De-coupling

So coming back to the principle, what is the problem here ? Our activity is doing too much. Not only does it have to display whatever about apples, it has to configure a request, pass it to a `RequestQueue` and manage the `RequestQueue`. That's too much. What our activity should be doing is asking for apples and showing it. That's all.

The solution is to use a `WebServiceManager` class. The activitiy asks this class for information and displays it. (This sample implementation also uses `EventBus` instead of interfaces).

    public class MyActivity extends Activity {
        @Inject WebServiceManager mServiceManager;
        @Inject EventBus mEventBus;

        @Override
        public void onCreate(Bundle savedInstanceState) {
            mServiceManager.getApples(); // or getApples(20)
        }

        public void onEvent(Apples[] apples) { // called when WebServiceManager pushes apples to EventBus
            // do something with apples
        }

        public void onEvent(WebServiceError error) { // called when WebServiceManager pushes an error to EventBus
            // do something to show error
        }

        @Override void onStart() {
            mEventBus.register(this); // must register to receive onEvent callbacks
        }

        @Override
        public void onStop() {
            mEventBus.unregister(this);
            mServiceManager.stop(); // Service manager should stop
        }
    }

Now our activity class doesn't know anything about what's happening with the WebService. No generics. Testing is even easier, just inject a subclass which overrides the methods called by the activity and push mock data to the bus (or mock error to test error handling). The mock class is literally a couple of method calls.
And finally, to change to a different low level implementation, just write a new WebServiceManager implementation and change the default injection to that... Boom! App changed over.

## Conclusion
This post was in the context of networking but the same principles hold for any service that you use. Write a wrapper for the service that is used throughout the app and then change the implementation over when you have a better one; inject it in and test away. 
I use this for ImageLoaders too so I can switch between say [`Picasso`](https://github.com/square/picasso) or the imageloader provided by Volley.

## Side Note
The only thing I don't really like about this setup is that I'm not using a wrapper for the `EventBus`. This means I can't really change over to a different bus easily. The reason I'm living with this for now is that the only other viable eventbus contender, [`Otto`](http://square.github.io/otto/) uses annotations and 