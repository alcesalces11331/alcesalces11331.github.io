---
layout: post
title:      "React Front-End, Rails-API Backend"
date:       2019-06-30 22:46:08 +0000
permalink:  react_front-end_rails-api_backend
---

# From Start To Finish

blah blah fucking blah here's the blog post to end all blog posts

The culmination of all I've learned has lead to this. My nascency to this. From learning the fundamentals of web development, I've progressed steadily and true to a burgeoning web developer. This project is the apex of all which came before. Platitudes aside, here's the real truth. I reached this point through a sheer amount of dedication and hard work. This project is nothing short of what someone can achieve with a passion to continue bettering themself and their work.

React is one of the most fun architectures to play with. It's responsive and intuitive. With Redux, managing persisted data becomes as simple calling your parents. With its lifecycle, managing what the user sees becomes a proverbial 'flick of the wrist'. Coding with react makes one feel like Merlin. This is not say this final project was easy, only that it was engrossing and challenging. Projects are **always** an experience to learn from and this one was no different. If anything, because of the complex layers required of it, this project was the ultimate experience to learn from. It requires knowledge of HTML/CSS, the bread and butter of the web. Any user will need to persist data. Learning from Sinatra, the capability of CRUD was like unlocking a horde of cache -- and putting it back together again. Our API, handled by Rails, was smooth, asking of correct RESTful routing and method calling. No errors here. The real Merlinesque manipulation was integrating the Javascript language -- accelerated along with ES6 -- into React's `fetch()` function and JSX. 

## Let's Have Some Fun

The project is required to incorporate a complete working knowledge of Container-Component style. It's required to have routes managed by `react-router `. HTML/CSS can be imported with, say, react-bootstrap, or own CSS. We've already covered what the Rails-API is supposed to do. It asks to `fetch()` data from an API, but here's where the fun can be had. With all projects I've done in the past year and a half, I've strived to make it as consuming as possible. My first [cli app](https://github.com/alcesalces11331/Rollin_Metzger-cli-app) draws data from [Hearthstone Top Decks](https://www.hearthstonetopdecks.com/) to draw and show information for the current meta decks. (Curiously of note, the single page 'style' was vastly useful to understanding how the react app would play out). Then, I've dabbled with Dungeons and Dragons content [here](https://github.com/alcesalces11331/Rollin_Metzger_Sinatra_Portfolio_Project), in a Sinatra app, and [here](https://github.com/alcesalces11331/Rollin_Metzger_RailsJS_Project) in a Javascript with Rails app. The common theme is one of embracing my interests and pushing the boundaries of a seemingly simple concept.

I did just that with this app. Another of my interests is the trading card game, Magic: The Gathering. For those unaware, it's the original trading card game which spawned an industry. Well, in pursuing possible topics for this project, I stumbled on this gem: [MTG Developers](https://magicthegathering.io). I was able to utilize a foreign API for this project. I was ecstatic. Choosing this topic created its own errors, which I'll detail below, but provided an excellent prop (pun intended) for education. 

The project itself is straightforward. The app will fetch data from https://api.magicthegathering.io/v1/sets/WAR/booster and then manipulate the data to be stored and presented for the user to interact with. This is a format of Magic: The Gathering called Limited. In essence, a player chooses one card from a set of cards (a booster pack) 40 times. They build their deck and play against other players using these cards. I wanted to show the user an interactive way to have mock drafts to choose and learn how to better their play for this format. 

### Getting Started

To make this project happen, I started with two commands:

The first command `create-react-app` loads all the dependencies I will need for the project without having to do all the configuration myself. I will do some manual configuration later to manage the store, but it was helpful to be able to expediate this process. This established the react side of the app. I still had to create the *how*, i.e., how would the react front-end load from the api *and* how would it call data from the store. Since the api and redux are intrinsically tied together, I figured I would start there.

Here's what I did to get the ball rolling:
```
rails new mtg-react-app --api
creat-react-app
```
To break it down, I instantiated a rails server and api  and navigated into it. *Then*, I called `create-react-app`. One of the tricky parts of this leg of the application was making use of a different pid for my server calls and the client calls. I took care of this with a few lines of code:
```
// procfile
web: cd client && npm start
api: bundle exec rails s -p 3001
```
This is called a procfile, which instructs the application to use two separate pids (connection ports) to better allow asynchronous calls to be processed. This creates its own problems which I fruitlessly tried to solve. It stems from Rails defaulting to utilizing SQLite3 as its database library. From what I learned (later on in the blog when I discuss creating cards and adding them to the store, I'll talk about this more in-depth) SQLite3 would attempt two POST requests. I would receive an error  `SQLite3::BusyException: database is locked:`. This is caused by SQLite3 being used to handle multiple connections. It's *possible* I had an errant Rails console open, but I thoroughly checked my connections and this was not the case. The culprit is the method being sent with the fetch request. My application was sending an OPTIONS request to my local API, which is not one of the simple requests: GET, POST, HEAD. Due to CORS policy, this is called a *preflight request* and is to ensure the request is safe. This preflight request to ensure safety is what was being sent *along with* the intended request. To completely get around this, in the future I will refactor mtg-react-app to utilize MySQL, which allows multiple connections to be made. 

Now, I had all my pieces put together in a broad sense. It's a bit like laying out the floorplan for a new house. I now knew where the walls were but I had to decided where to put my furniture. Or, to use a better analogy, following this route it like planting an oak -- our users will be squirrels. It's perfect and a bit a-corny.

### First Things First

I mentioned up above the main purpose of the app. I figured it was smart to ensure the main purpose was at least fetching the correct data. Here's the fetch action I set up, validating it worked with Postman:
```
// client/src/actions/DraftActions

export function fetchBooster() {
    return async (dispatch) => {
        dispatch({type: "LOADING_BOOSTER"});
        const proxyUrl = 'https://cors-anywhere.herokuapp.com/';
        const targetUrl = 'https://api.magicthegathering.io/v1/sets/WAR/booster';
        const response = await fetch(proxyUrl + targetUrl);
        const set = await response.json();
        const data = await set["cards"];
        return dispatch({
            type: 'FETCH_CARDS', payload: data
        });
    }
}
```
Notice I have to utilize a proxy to consistently make calls to Magic: The Gathering's API. This is due to the CORS policy regarding a cross-origin request. Lo and behold! Within Postman, I was having the promise resolved with no errors. This was part of the fun of programming this app. A [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) is a like a loan towards the future. It allows the call to be made without holding up any client-side rendering. It will continue to execute the promise until it is resolved. Then, the data is available and is processed accordingly. 

Ok, now that this action is working as it should, I moved to readying the drafting side of the reducer. While I was coding the reducer, I decided to go ahead and instantiate the store. Here's the code for the store:
```
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import { createStore, applyMiddleware, compose } from 'redux';
import rootReducer from './reducers/rootReducer';
import thunk from 'redux-thunk';
import './index.css';
import App from './App';

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;
const store = createStore(rootReducer, composeEnhancers(
    applyMiddleware(thunk)
));

ReactDOM.render(
    <Provider store={store}>
        <App />
    </Provider>,
    document.getElementById('root')
);
```
Utilizing a redux backend makes this app fly. It's so smooth. Initially, however, I was having issues. Redux-dev-tools was not detecting any store. It made me think, "Why is this happening?" I thought all of my code was correct, I was following all the Flatiron lessons and never saw anything different. I knew this was a great learning opportunity. I was excited. I learned about this little [gem](https://github.com/zalmoxisus/redux-devtools-extension). I had never witnessed composeEnhancers utilized, so I set up a variable to use compose or composeEnhancers: `const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;`. I then used this variable when creating the store in the very next line `const store = createStore(rootReducer, composeEnhancers(applyMiddleware(thunk)));`. This made use of *thunk* which is a middleware allowing the program to perform asynchronous calls. Finally, by using Provider, I was able to make the store accessible to *any* nested component wrapped in the connect() function

But, I had yet to develop the rootReducer, which I could easily create and update as I progressed on the app. Creating the rootReducer drew upon knowledge we had covered in the lessons and labs leading up to this project:
```
import draftingReducer from './draftingReducer';
import deckReducer from './deckReducer';
import cardReducer from './cardReducer';
import { combineReducers } from 'redux';

const rootReducer = combineReducers({
    drafts: draftingReducer,
    decks: deckReducer,
    cards: cardReducer
})

export default rootReducer;
```
This is the completed alpha version. I combined all the reducers using combineReducers(). Below is the draftingReducer, which finishes the making use of the Magic: The Gathering api.
```
// draftingReducer
function draftingReducer(state = {
    loading: false,
    draftingData: []
}, action) {
    switch (action.type) {
        case "LOADING_BOOSTER":
            return {...state, loading: true, draftingData: [], }
        
        case "FETCH_CARDS":
            return {...state, loading: false, draftingData: action.payload}

        default:
            return state
    };
};

export default draftingReducer;
```
When coding this portion of the project, I loved how easy it was to access our data. I had a few choices here. I could make use of  `mapStateToProps` to access the store from any reducer wrapped with the connect() function. I could call specific actions from the reducers using `mapDispatchToProps`, but for the simplicity of the alpha version I found it more efficient to call specific functions from the actions instead. I incorporated flexible scalability to make use of `mapDispatchToProps` when I add greater complexity to the application. 

### Drafting

We had collected the necessary parts of the program to begin drafting. Following container/component practices, I knew I wanted to have my CardsContainer handle all of the logic. That said, let's take a look at how I accomplished this.
```
class CardsContainer extends Component {
    constructor(props){
        super(props);
        this.renderCardsProps = this.renderCardsProps.bind(this)
        this.state = {
            cards: [],
            cardCount: 0
        }
    }

    render() {
        return (
            <div>
               <button onClick={() => this.handleFetchBooster()}>Open a Pack</button>
            </div>
            
        )   
    } 
}
```
I first created the container knowing I would first hard-code the cards chosen from the opened packs. I bound renderCardsProps because -- as I'll show later -- in return() I'm calling a function from *this*. Before I created a function to map the card objects to the CardsComponent, I needed to first create a function to make a fetch request to ` 'https://api.magicthegathering.io/v1/sets/WAR/booster'`, handleFetchBooster():
```
handleFetchBooster() {
        this.props.fetchBooster();    
    };
```
To make use of this, I had to add a few more lines of code:
```
import { fetchBooster } from '../actions/DraftActions';
```
and
```
export default connect(null, { fetchBooster })(CardsContainer);
```
Having this function successfully returning the integral requests, I then moved into building exactly how CardsContainer would persist the data and render the data. 

Moving forward, I wanted to first render the data for the user. This required implementing Cards, the component side of of CardsContainer:
```
const Card = props => <div>
    <ul>
        <div className="mtg-card">
            <li id="mtg-card-name" onClick={(e) => props.handleAddCard(e)} cardid={props.cardId}>{props.name}</li>
            <li id="mtg-card-manaCost">{props.manaCost}</li>
            <li id="mtg-card-text">{props.text}</li>
        </div>
        
    </ul>
</div>

export default Card;
```
I knew it was going to be stateless, so I created a presentational component. It receives props from CardsContainer and renders them to the web page. I also knew it was going to have to somehow be 'clickable', i.e., I be responsive to user input. Back in CardsContainer, I would add two functions: handleAddCard() and renderCardsProps():
```
renderCardsProps() {
        const cardProps = this.props.draftObjects.draftingData;
        if ( this.state.cardCount < 40 ) {
        return cardProps.map(
            idvCard => <Card key={idvCard.id} cardId={idvCard.id} name={idvCard.name} text={idvCard.text} 
						manaCost={idvCard.manaCost} handleAddCard={(e) => this.handleAddCard(e)} />
        )} else {
            return <h3>Your Deck Is Complete</h3>
        }
    }
```
Walking through it, the function takes the data we've fetched from MTG's api, and render it *only* if our counter is less than 40. If this is true, it will map() the data from the store to dynamically render all the cards. To make this necessary, a number of additions needed to be created. It is important to take a moment to highlight react's focus on unique keys. React uses keys [to identify which items have changed, added, or removed](https://reactjs.org/docs/lists-and-keys.html). Why is this important? It has to do with reconciliation and the docs on it are found [here](https://reactjs.org/docs/reconciliation.html#recursing-on-children). Briefly, it is how react handles large quantities of iterations for possible mutations. When a dom has hundreds if not thousands of children, react doesn't have to mutate every child. It quickens the processing and makes the app that much more efficient. Besides, if you don't create unique keys react throws an error tantrum for every non-unique child.

Continuing on, I will utilize mapStateToProps() to obtain the data fetched from the button, "Open Pack", is clicked:
```
const mapStateToProps = state => {
    return {
        draftObjects: state.drafts,
    }
}

export default connect(mapStateToProps, { fetchBooster })(CardsContainer);
```
And then, in render(), I will call renderCardsProps():
```
<div className="mtg-cards">
    {this.renderCardsProps()}
</div>
```
Now, the data we want to show our is user is rendering correctly. But, we also want to persist the data to our store. To persist the chosen data, I mentioned above I created a function called `handleAddCard()`. It would have to do two things: take in the chosen data and then submit a post request to our Rails API. Here's the function:
```
handleAddCard(e) {
        const cardName = e.target.innerText;
        const id = e.target.attributes.cardid.value;       
        this.props.createCard(cardName, id);
        this.setState({
            cards: [...this.state.cards, cardName]
        });
        if ( this.state.cardCount < 40 ) {
            this.handleFetchBooster();
            this.handleCardCounter();
        }    
    }
```
handleAddCard() takes in one argument, *e*. This is passed from Card.js, the component who's sole purpose is to render the props from the opened booster pack. Within the presentational component, I've passed `handleAddCard()` as a prop so when the user chooses a card the function is called. I then am able to extract the data from the card I will pass to the connected function `createCard()`, which takes in two arguments: name, and id. To do this, here's the updated import and export lines:
```
import { createCard } from '../actions/CardActions';
export default connect(mapStateToProps, { createCard, fetchBooster })(CardsContainer);
```
And here's *createCard()* from the *CardActions.js* file:
```
export function createCard(name, id) {
    return async dispatch => {
        const response = await fetch('http://localhost:3001/api/cards', {
            method: 'POST',
            headers: { "Content-Type": "application/json", "Access-Control-Allow-Origin": "http://localhost:3000" },
            body: JSON.stringify({name, id})
        });  
        const payload = await response.json();
        dispatch({ type: "CREATE_CARD", payload });
    };
};
```
As I mentioned above, within the headers of *createCard()* I have to tell the API to allow access from the client side: localhost:3000 while the actual response is to the server: localhost:3001/api/cards. Then, it's simple a ruby method within the Cards controller to actually handle the response. Quick and easy. 

However, *handleAddCard()* will only render another booster *if* the internal counter is less than 40. This has been coded into *CardContainer.js* and for true management of the amount of cards in a deck will need to be integrated into a call to the Deck branch; it will need to be rendered in a higher parent container and passed as a prop down to *CardContainer*. As of right now, the counter resets when the container is derendered, like when the user views the deck of their chosen cards or goes back to the home page. But, this is still alpha (if it can even be called alpha). 

### Deck and the Rest

I briefly mentioned the cards the user chooses are added to the store and persisted. The cards are then picked up by *DeckContainer.js* with *renderCardsProps()*:
```
renderCardsProps() {
        if ( cardProps !== undefined ) {
            return cardProps.map(
                idvCard => <Deck key={idvCard.multiverseid} name={idvCard.name} />
            )
        }
    };
```
*renderCardsProps()* has a sole purpose of receiving the props from *mapStateToProps* and returning the props mapped -- similary to *Card.js* -- *Deck.js*, another presentational component, nearly identical to *Card.js*. It utilizes a conditional to determine if the actual card data is undefined. This will be altered in future versions as it is incomplete and fails to fulfill its purpose. Its purpose is to filter the cards added as errors as I mentioned up above where I discuss preflight requests and the locking up of the rails server. When the server receives those two requests, it adds *both* the actual card object and the error object, thus causing both of them to be rendered by *DeckContainer.js*. This can be easily fixed with changing the database from SQLite3 to MYSQL. It can also be changed by adding a conditional to the "CREATE_CARD" case in *CardsReducer.js*.

Moving on, I wanted the user to be able to completely reset their deck when they were finished creating it. The rest of *DeckContainer.js* is coded to handle the action of deleting the deck. This involves *handleOnClick()* and the requisite route creation function *handleLinkRoute()*. With all this coded, the user is able to view and delete their deck. 

#### The Rest

With the bulk of the application up and running, it was time to create more presentational components for all the links. This went smoothly. I created components for: About, Contact, Header, and Footer. These were loaded by *AppRouter.js* and stuck around when the user would be navigating from render to render. I chose to utilize an AppRouter container on top of *App.js* because CSS applied to App.js extends only to the section of the webpage it renders. When all the client containers are inserted within *AppRouter.js* the applied CSS filled the whole page as I wanted it to. 

When coding this very last section, I ran into the "React white screen of death". It cost me many hours and frustration. It was followed by many humbling laughs. What happened was I was experimenting making use of react-router-dom. *AppRouter.js* was the top container for links and routing, so, naturally, it was where the necessary imports and uses of Router and routes were defined. However, as I soon realized, two instances of Router -- say, one rendered in Header.js, the presentational component holding links -- create an incomprehensible loop for React to figure out. The true confusing issue was when the console would output, "Compiling complete" without outputting any errors. Without simply commenting out the added Header import code, I was running around in the white. However, through my folly, I learned quite a bit about Router, which is all I could ask for. 

## Wrapping Up

Learning to develop a full-stack application has been a fulfilling achievement. I've learned a lot about more than programming though. Programming takes persistence. It takes tenacity. It takes enthusiasm and curiosity. How else is learning supposed to take place? 

Here's the link to my github: [Github](https://github.com/alcesalces11331)
Here's a link to this application: [mtg-react-app](https://github.com/alcesalces11331/Flatiron-React-Project/tree/master/mtg-react-app)
