---
layout: post
title:      "React Powered Club"
date:       2020-04-20 03:28:16 -0400
permalink:  react_powered_club
---

[The Library](https://github.com/ncaudill27/the-library) is a nice quick way to kick-start a book club and begin discussing your current read with friends!

This project was a lot of fun to build. What seemed a fairly simple concept at first quickly became a first hand look at just how multi-faceted software development can be. Overall working with React and Redux was a great learning experience.

## Main Features
1. Fast JSON API serialization
2. Heavy reliance on Redux store
3. Specialized and reusable React components
4. JSON Web Token session tracking and authentication
5. Full-stack build using proxy middleware
6. Interactive, fluid UI.
7. Data from NYTimes and Google API

## Setting Up
___
From the start I knew this project had the potential to become more than just a simple project to throw together. Preferring to have an idea of the data to be used the first task was to get access to that data.

Having used the API in one the Flatiron labs, hitting the [New York Times Books API](https://developer.nytimes.com/docs/books-product/1/overview) was easy enough.

[Google's Books API](https://developers.google.com/books/docs/overview) was slightly trickier. Browsing their developer tools and references gives a good taste of how deep server-side APIs can go.

Building React components to query the APIs felt like opening the instructions to a new LEGO project. You know what the end product is supposed to be, but not by looking at an individual section.


Regardless, now I had real JSON objects in hand. On to map out some models. With the *"very basic"* idea that a User could join a Club and that Club would have multiple Threads to Comment on. It became clear this application would have many layers. Books hadn't even been drawn in yet.

With that in mind the next logical step was to draw out what a Club's show page might look like. A sidebar/main combo seemed to be the appropriate approach. Sketching a "wish list" of a presentation really got the ball rolling. It is a visual representation of the components that would be needed.

## The Process
___
For anyone hasn't read [Thinking in React](https://reactjs.org/docs/thinking-in-react.html) I highly recommend it.

Building out systematically starting with static components meant having data. Again, having real structures being my comfort zone. Playing with Rails, Fast JSON, and having nice hefty seed file felt right.

Up until the point where I realized I had no idea where or how I wanted the information fetched out. So, whereas big felt right in the backend. Small felt right on the frontend. Creating the small components that would be repeated throughout the application was a simple enough task to stay busy. I wasn't sure how the data would flow, but I knew where it would end up.

```
const InputField = ({handleSubmit}) => (
  <div className='input-field'>
    <input type='text' onChange={} />
    <button onClick={handleSubmit} >Click me!</button>
  </div>
);
```

Components like Comment, Avatar, InputField quickly expanded into ClubList, UserBox, NavBar. Which in turn grew into ClubContainer, ThreadList. While, filled with placeholders and pseudocode, the application began to take life.

Once one model was connected through Redux the others fell into place, choosing combineReducers to maintain separation of concerns. With actual data the components evolved into something that actually felt React-like. Components became specialized and efficient.

```
function Input({name, value, handleChange}) {
  switch(name) {

    case "password":
    case "confirmPassword":
      return <input name={name} type='password' onChange={handleChange} value={value} autoComplete='off' />;

    case "description":
    case "bio":
      return <textarea name={name} onChange={handleChange}>{value}</textarea>;

    default:
      return <input name={name} type='text' onChange={handleChange} value={value} autoComplete='off' />;
  };
}
```
Working incrementally is overrated though right? Who likes flow-states?

## JSON Web Tokens
___
Oh boy. Where to start? This next section I hope helps anyone considering adding tokens to their workflow. First of all having tokens does make any user authentication much much nicer. However, getting there is the trick.

There many **so** many sources, some of them very opinionated. I came to the conclusion that there was no *easy/beginner* way in so I began to read, *a lot*.

These are some of the resources I found most helpful.

[A nice fly by walkthrough](https://medium.com/@micah.shute/react-front-end-rails-server-a-guide-20f19488dac5) on set up and security from Flatiron coach Micah Shute.

[A good example of the opposing side](https://dev.to/rdegges/please-stop-using-local-storage-1i04) and why *not* to use JWT.

My go to. [A thorough approach to one implementation](https://levelup.gitconnected.com/jwt-auth-in-a-react-rails-app-8a7e6ba1ac0) of tokens. Which I just now realize was also written by a Flatiron coach, Reinald Reynoso.

Finally, the readme files for the [JWT](https://github.com/jwt/ruby-jwt) and [JSON Web Token](https://github.com/garyf/json_web_token) gems.

To summarize in one paragraph:
Transmitted data can be easily intercepted. Securing/encrypting this information is essential to man in the middle attacks. JWTs are a means to securely transmit information as an alternative to API-side session tracking. They can be broken down into three parts
1. A header containing algorithm and identifying information.
2. The payload. Contains the information being passed back and forth.
3. The signature. Encoded versions of the header + payload + a server side secret.

Ultimately I decided on JWT not just for the sake of learning and practice. But also with the hope of adding websockets and taking of advantage of OAuth2 and the Google API I'm already connected to.

At the this point I feel very far from identifying best practices. What I do know is implenting JWT was a very satisfying hurdle to get over. As, by design it is intentionally strict in it's implementation.

## Scaling
___
Planning for a project should be done actively. Taking into account not just original mapping and structure ideas, but also the actual work and standing point of the project as it is. This lesson was learned the hard way.

Having access the JWT gave me the idea that I could stray from the substantial Redux store I had built and keep the session user on the front end simply passed down through props. My thought process centered around the idea that the UI rendered would be dependant on a current user either way.

Why not keep it in local state and fetch the user on componentDidMount with the token?

I lost about two days on that misplay eventually refactoring all the session related fetch requests back into Redux and adding a currentUser key to the users branch in the store.

At this point was when I realized first-hand just how time consuming refactoring a conceptual idea can be when a project has grown. Especially considering that it was mostly just moving fetch requests. Side effects were usually limited to digging through one callback.

With this is mind I will go through the effort of learning how to plan in stages. Beginning with mapping the current state of the project. Logging current inefficiencies, areas where I know the code could be more DRY or don't fully understand.

Considering, I expect on expanding this project into the closest replica of a working website (notifications, in-depth error handling, OAuth login, deeper use of Google's API) diligent planning is crucial.

The end game is Heroku deployment with a clean, easily maintainable version 0.1. As enjoyable as that is, it won't get me where I need.

One LEGO at a time.
