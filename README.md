# Final Project | Fetch API

### Find a Mental Health Therapist :herb:

I've created a website, which fetches Random User Data from an API to give users access to available therapists and their contact information. I'm using the Random User Generator Data as a placement holder for therapists' e-mail addresses and current location.

## Idea

As an advocate for mental health, I wanted to create a website where users can easily find a mental health therapist. Users are introduced to the homepage, which explains the service. Then, users are prompted to search for a therapist, which they can do by clicking "Get matched now!" or the "Find a Therapist" button in the navigation.


## Design

### Responsive Design

Keeping in mind that websites need to mobile and desktop friendly, I used responsive units in my CSS.

```css
@media screen and (max-width: 400px) {
  h1 {
    font-size: 1rem;
  }

  .user-profile {
    margin: 0;
    margin-top: 2rem;
    width: 100%; 
    height: 11rem;
    background: #315b86;
    border-radius: .3em;
  }

```

## JavaScript

This is the JS used to fetch data from the API.

I **declared** and **initialized** a variable called url and assigned it the value.

```javascript
const url =' https://randomuser.me/api/?nat=us';
```

Here I'm grabbing the HTML element and setting it to the respective variables.

```javascript
let fullname = document.getElementById('fullname');
let username = document.getElementById('username');
let email = document.getElementById('email');
let city = document.getElementById('city');
let btn = document.getElementById('btn');
```

As soon as the user clicks the button, it calls the listener function.

```javascript
btn.addEventListener("click", function() {
    fetch(url)
      .then(handleErrors)
      .then(parseJSON)
      .then(updateProfile)
      .catch(printError)
  });
```

Here, I've set the values coming back from the API to the innerHTML.

```javascript
fullname.innerHTML = profile.results[0].name.first +" "+profile.results[0].name.last;
```

When the user clicks “Keep Looking” it will make a GET request to the API that returns the contact information of a therapist that's available. This is an example of a response coming back from the API that I use to show the data.

```javascript
{"results":[{"gender":"female","name":{"title":"Ms","first":"Christina","last":"Porter"},"location":{"street":{"number":8086,"name":"Walnut Hill Ln"},"city":"Columbia","state":"Michigan","country":"United States","postcode":76356,"coordinates":{"latitude":"-54.6769","longitude":"66.7563"},"timezone":{"offset":"-8:00","description":"Pacific Time (US & Canada)"}},"email":"christina.porter@example.com","login":{"uuid":"3bb2cf36-b536-4783-8634-e36097649b78","username":"crazytiger282","password":"camden","salt":"wpADFodz","md5":"bbe5d6813649a590124ddfa57117c6e2","sha1":"f26df383ee3a66accb3fe7ef0aca4ecec99b0a3a","sha256":"db94ef4798c0e5122da5fdc1b489ea6b630a705e1975dff393c5655d6ac5edd3"},"dob":{"date":"1965-08-19T11:46:23.466Z","age":55},"registered":{"date":"2002-10-10T03:07:47.427Z","age":18},"phone":"(442)-574-5766","cell":"(109)-285-1759","id":{"name":"SSN","value":"976-40-9750"},"picture":{"large":"https://randomuser.me/api/portraits/women/60.jpg","medium":"https://randomuser.me/api/portraits/med/women/60.jpg","thumbnail":"https://randomuser.me/api/portraits/thumb/women/60.jpg"},"nat":"US"}],"info":{"seed":"1e8337c55a3ffa8f","results":1,"page":1,"version":"1.3"}}
```

This is how I plugged in the information.

```javascript
  function updateProfile (profile){
    avatar.src = profile.results[0].picture.medium;
    fullname.innerHTML = profile.results[0].name.first +" "+profile.results[0].name.last; 
    username.innerHTML = profile.results[0].login.username; 
    email.innerHTML = profile.results[0].email;
    city.innerHTML = profile.results[0].location.city;
    return 1;
  }
```

After I fall fetch, the first thing I do is check for errors.

```javascript
  function handleErrors (res){
    if(!res.ok){
      throw error(res.status);
    }
```

This calls my handle error function.
It then parses the response and returns the response in JSON format 

```javascript
  function parseJSON (res){
    return res.json();
  }
```

Then, I use `updateProfile` and display it on the HTML file.
```javascript
  function updateProfile (profile){
    avatar.src = profile.results[0].picture.medium;
    fullname.innerHTML = profile.results[0].name.first +" "+profile.results[0].name.last; 
    username.innerHTML = profile.results[0].login.username; 
    email.innerHTML = profile.results[0].email;
    city.innerHTML = profile.results[0].location.city;
    return 1;
  }
 ```

If there is an error with the request to the API, the errors are logged in the console.

```javascript
  function printError (error){
    console.log(error);
  }
```


## Built With

* [Visual Studio Code](https://code.visualstudio.com/)

## Resources

• [Random User Generator](https://randomuser.me/)

• [Professor Maria Campbell's Fetch Geo IP API](https://interglobalmedia.github.io/fetch-geo-ip-api/#/)
