# 2. Timeouts

Imagine you're trying to call a friend on the phone, but he doesn't answer. You don't want to wait forever, so you decide to hang up after a certain amount of time. In computing, a timeout is similar: it's a limit on how long you wait for an action to complete before giving up.

Timeouts are like setting a timer for how long you're willing to wait for something to happen. If the timer runs out and the action isn't done, you stop waiting and move on.

## Fast Failures:

Fast failures happen quickly, so you know right away that something went wrong.

**Example:** If you call a friend and get a busy signal immediately, you know you can't talk to them right now.

- Quickly indicate that something is wrong.
- Allow systems to recover and try again sooner.

## Slow Failures:

Slow failures take a long time, and you might have to wait a while before finding out there's a problem.

**Example:** If you call a friend and the phone just keeps ringing without an answer, you only find out after waiting that you can't talk to them.

- Can cause delays and frustration.
- May waste resources by waiting too long.

## Connection Timeouts:

A connection timeout is how long you wait to establish a connection with another computer or server.

**Example:** Think of it like waiting for your friend to pick up the phone. If they don't pick up in a certain amount of time, you hang up.

- Set a limit on how long to wait for a connection.
- Help avoid long waits when a server is down or unreachable.

## Request Timeouts:

A request timeout is how long you wait for a response after you've made a request.

**Example:** Imagine you asked your friend a question on the phone and are waiting for their answer. If they take too long, you decide to end the call.

- Limit how long to wait for a response after a request is made.
- Prevent your system from hanging indefinitely while waiting.

## Summary

Timeouts are like setting a timer for how long you're willing to wait for an action to complete. Fast failures happen quickly, while slow failures take longer. Connection timeouts limit how long to wait to establish a connection, and request timeouts limit how long to wait for a response after making a request. These concepts help ensure systems remain responsive and efficient.
