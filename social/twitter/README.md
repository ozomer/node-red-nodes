node-red-node-twitter
=====================

<a href="http://nodered.org" target="_new">Node-RED</a> nodes to talk to Twitter.

The Twitter API will **NOT** deliver 100% of all tweets. This does **NOT** give access to the Twitter Firehose.

Tweets of who you follow will include their retweets and favourites.

**Note** : This is the same node as was in the core of Node-RED.
As of v0.10.8 it will be installed from here instead.

Install
-------

Run the following command in the root directory of your Node-RED install, usually
this is ~/.node-red .

        npm install node-red-node-twitter

Usage
-----

Provides two nodes - one to receive messages, and one to send.

###Input

Twitter input node. Can be used to search either:

 - the public or a user's stream for tweets containing the configured search term
 - all tweets by specific users
 - direct messages received by the authenticated user

Use **space** for *and*, and **comma** , for *or* when searching for multiple terms.

Sets the **msg.topic** to *tweets/* and then appends the senders screen name.

Sets **msg.location** to the tweeters location if known.

Sets **msg.tweet** to the full tweet object as documented by <a href="https://dev.twitter.com/docs/platform-objects/tweets">Twitter</a>.

**Note:** when set to a specific user's tweets, or your direct messages, the node is subject to
Twitter's API rate limiting. If you deploy the flows multiple times within a 15 minute window, you may
exceed the limit and will see errors from the node. These errors will clear when the current 15 minute window
passes.


###Output

Tweets the **msg.payload**.

To send a Direct Message (DM) - use a payload like.

        D {username} {message}

If **msg.media** exists and is a Buffer object, this node will treat it as an image and attach it to the tweet.

If **msg.params** exists and is an object of name:value pairs, this node will treat it as parameters for the update request.
