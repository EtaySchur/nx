# RxJS Lab 4: Create a custom Observable

### Scenario

Now that performance and race-conditions have been addressed, let's explore creating observables and stopping the **observable execution**. We will also explore how an observable can be shared and the impacts of the sharing.

![image](https://user-images.githubusercontent.com/210413/48207479-93564600-e325-11e8-9663-d35903ff83b7.png)

We will create a custom Observable that emits a ticker value.<br/>
And then we will use that observable [in the `TicketTimerService`] as an Observable API.

<br/>

---

<br/>

### Code Instructions

1. Use the Angular CLI to generate a new `TicketTimerService` in the `client-customer-portal-tickets-feature` lib.

##### In `libs/client/customer-portal/tickets-feature/src/lib/ticket-timer.service.ts`

1. Create a class field for a `timer$ : Observable<number>` and instantiate a custom observable.
2. In the Observable Execution area, set up a count variable and use `setInterval` to increment it every `1000ms`. Make a call to `observer.next` in the setInterval callback and emit the current counter value.
3. Capture the handle to the `setInterval` and use it when creating a _teardown_ function. Teardown functions are needed to clean up producer activity when the observer unsubscribes. In this case, we need to return a function that clears the interval with `clearInterval`).

##### In `ticket-details.component.ts`

4. Inject the service into the `constructor`. When the "Start a Timer" button is clicked, set the `timer$` class field to the `timer$` property in the `TicketTimerService` object .

### Code Snippets

###### `ticket-timer.service.ts`

![ticket-timer.service.ts](https://user-images.githubusercontent.com/210413/47941498-5d940600-debc-11e8-88c9-46fb2178d318.png)

###### `ticket-details.component.ts`

![ticket-details.component.ts](https://user-images.githubusercontent.com/210413/47941597-c3808d80-debc-11e8-8b30-e9510ceea1d1.png)

###### `ticket-details.component.html`

![rxjs4 3](https://user-images.githubusercontent.com/210413/47622803-5e512480-dad7-11e8-9091-defca17547fe.jpg)

<br/>

### Bonus Exercise

- Set up an array of `Observable<number>` as timers and push the `TicketTimer` service timer into it.
- Then update the template to `ngFor` the timers and use the async pipe to display each timer value.

<br/>

---

<br/>

### Investigate

Run the application and:

- Start the timer... see the timer values increment.
- Route to a different view and return to the `TicketDetailsComponent`, confirm the timer is no longer working.

**Questions**:

- Why does the timer stop on routing?
- What happens when you navigate away from the ticket?
- Why does the start timer not start immediately after clicking?

Add a `console.log()` in the teardown function of your TicketTimerService. Trying navigating again and watch the console.

<br/>

### Next Lab

Go to RxJS Lab #5: [Use Mulitcast BehaviorSubject](lab-5.md)
