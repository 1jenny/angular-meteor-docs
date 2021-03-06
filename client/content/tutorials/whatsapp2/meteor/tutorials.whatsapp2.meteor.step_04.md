{{#template name="tutorials.whatsapp2.meteor.step_04.md"}}

In this step we will add the messages view and the ability to send messages.

Before we implement anything related to the messages pages, we first have to make sure that once we click on a chat item in the chats page, we will be promoted into its corresponding messages view.

Let's first implement the `showMessages()` method in the chats component

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.1"}}

And let's register the click event in the view:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.2"}}

Notice how we used we used a controller called `NavController`. The NavController is `Ionic`'s new method to navigate in our app, we can also use a traditional router, but since in a mobile app we have no access to the url bar, this might come more in handy. You can read more about the NavController [here](http://ionicframework.com/docs/v2/api/components/nav/NavController/).

Let's go ahead and implement the messages component. We'll call it `MessagesPage`:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.3"}}

As you can see, in order to get the chat's id we used the `NavParams` service. This is a simple service which gives you access to a key-value storage containing all the parameters we've passed using the NavController. For more information about the NavParams service, see the following [link](http://ionicframework.com/docs/v2/api/components/nav/NavParams).

Now it has to be added to AppModule:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.4"}}

We've used `MessagesPage` in `ChatsComponent` but we haven't imported it yet, let's make it now:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.5"}}

Now we can add some data to the component. We need a title and a picture to use inside the chat window. 
We also need a message:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.6"}}

As you probably noticed, we added the ownership for each message. 
We're not able to determine the author of a message so we mark every even message as ours.

Let's add the `ownership` property to the model:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.7"}}

One thing missing, the template:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.8"}}

The template has a picture and a title inside the Navigation Bar. 
It has also two buttons. Purpose of the first one is to send an attachement. The second one, just like in Chats, is to show more options.
As the content, we used list of messages.

It doesn't look quite good as it should, let's add some style:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.9"}}

Now we can add it to the component:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.10"}}

This style requires us to add some assets, first we will create a copy called `assets` inside a `public` directory and then we will copy them like so:

    $ mkdir public/assets
    $ cd public/assets
    $ wget https://github.com/DAB0mB/ionic2-meteor-messenger/blob/master/www/assets/chat-background.jpg
    $ wget https://github.com/DAB0mB/ionic2-meteor-messenger/blob/master/www/assets/message-mine.jpg
    $ wget https://github.com/DAB0mB/ionic2-meteor-messenger/blob/master/www/assets/message-other.jpg

Now we need to take care of the message's timestamp and format it, then again we gonna use `angular2-moment` only this time we gonna use a different format using the `AmDateFormat` pipe:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.12"}}


Our messages are set, but there is one really important feature missing and that's sending messages. Let's implement our message editor.

We will start with the view itself. We will add an input for editing our messages, a `send` button, and a `record` button whos logic won't be implemented in this tutorial since we only wanna focus on the text messaging system. To fulfill this layout we gonna use a tool-bar (`ion-toolbar`) inside a footer (`ion-footer`) and place it underneath the content of the view:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.13"}}

Our stylesheet requires few adjustments as well:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.14"}}

Now we can add handle message sending inside the component:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.15"}}

As you can see, we used `addMessage` Method, which doesn't exist yet.

It the method which will add messages to our messages collection and run on both client's local cache and server. We're going to create a `server/imports/methods/methods.ts` file in our server and implement this method:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.16"}}

It's not yet visible by server, let's change it:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.17"}}

We would also like to validate some data sent to methods we define.
For this we're going to use a utility package provided to us by Meteor and it's called `check`. Let's add it to the server:

    $ meteor add check

And we're going use it in our method we just defined:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.19"}}

The `nonEmptyString` function checks if provided value is a String and if it's not empty.

In addition, we would like the view to auto-scroll down whenever a new message is added:

{{> DiffBox tutorialName="whatsapp2-meteor-tutorial" step="4.20"}}


This is how the messages view should like:

> *android* {{tutorialImage 'whatsapp2' 'screenshot-3-md.png' 500}}

> *ios* {{tutorialImage 'whatsapp2' 'screenshot-3-ios.png' 500}}

{{/template}}