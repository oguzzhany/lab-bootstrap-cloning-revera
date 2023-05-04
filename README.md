![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# LAB | Bootstrap Cloning Revera

Internet provides lots of templates and themes. But some of them cost money. However, we don't need to pay for something we already know how to do, so... We are cloning a theme!

[Revera Theme](https://web.archive.org/web/20180109051150/http://demo.fabthemes.com/revera/)

![Revera Picture](https://i.imgur.com/3y7yay8.png)

As we can see, this template is a very good example of the type of webpages we can see on the Internet. With Bootstrap, we are able, in barely a few hours, to copy the appearance of this template.

## Requirements

- [Fork this repo](https://guides.github.com/activities/forking/)
- Clone this repo into your `~/code/labs`

## Submission

Upon completion, run the following commands
```
$ git add .
$ git commit -m "done"
$ git push origin master
```
Navigate to your repo and create a Pull Request -from your master branch to the original repository master branch.

In the Pull request name, add your name and last names separated by a dash "-"

## Deliverables

Your page should look like the original one as much as possible. You should push every resource needed to make it work properly. Please, organize your code and your files carefully.

## Iteration 1: General layout

Focus on the general layout. What do we mean by general? Most of you are thinking about the header, how to create the menu, whether you should use 2 columns for a link or maybe 3... Don't worry, this is a common mistake at the beginning. However, as we will see, the best way to approach it is to look at the big “boxes” first and don't lose ourselves on the details.

So we have to see the page as a big container and identify the most important sections. Here you have an example:

![general layout](https://i.imgur.com/IIAG0g0.jpg)

Remember to use the inspector to determine the width and the height of the Revera page. Also, we could find out which Bootstrap classes have been used and anything else that is necessary to make our page looks like the original.

One cool Boostrap feature is that you have three elements that make our lives easier: `container`,  `row` and `columns`. Don't hesitate to use them!

## Iteration 2: Internal structure

Now that we have a global vision of the page, we can go to the second level, dividing our box into their own internal structure. This means that if you previously created a single container and various rows, now we are going to define the columns. You will have to estimate the number of cells you will need in each row.

The [grid system](https://getbootstrap.com/docs/5.2/layout/grid/) of Bootstrap gives you all the `.col` classes. Remember that each row has a size of 12 columns.

## Iteration 3: Include the content

Really cool! Now, you need to insert the content in its respective places (text, images, ...) and change some CSS options like margins, paddings, etc. to finish the template. It´s just a matter of Bootstrap!

Well... Maybe it's not that easy. But try different things and make it happen!

Happy Coding!

# blockbuster-remix
<br>

## Description
Rent platform for video games from local owners.
<br>

## User stories
- **404** - As a user I want to see a nice 404 page when I go to a page that doesn’t exist so that I know it was my fault.
- **500** - As a user I want to see a nice error page when the super team screws it up so that I know that is not my fault
- **login-signup** - As a user I want to see a welcome page that gives me the option to either log in as an existing user, or sign up with a new account. 
- **add-signup** - As a user I want to sign up with my full information so that I can safely rent video games from people.
- **homepage** - As a user I want to see a notifications preview and be able to either search a video game by console, or go to my profile from the home page.
- **game-search-results** - As a user I want to see the search results with a oreview image, the title, the console it's for, and the price of rent per day. Also, to go back to the home page if I don't want to see that search anymore.
- **game-rent-form** - As a user I want to see more information about the game when I click on a certain item, the renter's general location, and to choose how many days I want to rent a game. Also, to go back to the search results page if I don't want to see that item anymore.
- **success** - As a user I want to see a success page that details the contact information with the renter and confirmation of the general information of the game I just rented. Also, to go back to the home page when I'm done.
- **user-profile** - As a user I want to check my profile information and be able to edit it, and add new games to my renting library. Also, to go back to the home page if I don't want to see the profile anymore.
- **notifications** - As a user I want to check my notifications in-depth, to see who has rented my game and games I have rented.
<br>

## API routes (back-end)

- GET / 
  - renders login-signup.hbs
- GET /auth/signup
  - redirects to / if user logged in
  - renders add-signup.hbs
- POST /auth/signup
  - redirects to / if user logged in
  - body:
    - email
    - password
    - full name
    - birthday
    - gender
    - address
    - phone
    - cardInfo
    - typeOfCard
    - cardNumber
    - expDate
    - CVV
- POST /auth/login
  - redirects to / if user logged in
  - body:
    - email
    - password
- POST /auth/logout
  - body: (empty)

- GET /
  - renders homepage.hbs (the profile preview + search form)
- POST /homepage (search action)
  - body: 
    - game-title
    - console
- GET /game-search-results
  - renders game-search-results.hbs
  - includes the list of games
  - redirects to / if user presses button
- GET /rent-form/:id
  - renders rent-form.hbs
  - redirects to /game-search-results if user presses button
- POST /rent-form/:id
  - body: 
     - days
     - price update
- GET /success
  - renders success.hbs
  - redirects to / if user presses button
  
- GET /profile
  - renders user-profile.hbs
  - redirects to / if user presses button
- POST /profile (to edit profile)
  - redirects to /add-signup (we reuse it but for edit purposes)
  - body:
    - email
    - password
    - full name
    - birthday
    - gender
    - address
    - phone
    - cardInfo
    - typeOfCard
    - cardNumber
    - expDate
    - CVV
- POST /profile (to add game)
  - body:
    - game title
    - console
    - price
    - max days of rent
- GET /profile
  - renders user-profile.hbs updated
  - redirects to / if user presses button
- GET /notifications
  - renders notifications.hbs
  - redirects to / if user presses button
- GET /success (for renter)
  - renders success.hbs
  - redirects to /notifications if user presses button

<br>

## Models
 
 - User 
    new Schema ({
     	_id: ,
     	email: String, required: true,
      password: String, minlength: 6, maxlength: 12,
     	fullName: String, required: true, maxlength: 20,
      birthday: Date,
      gender: String, ENUM[M,F,other]
      address: String, required: true, maxlength: 30,
      phone: String, required: true, minlength: 9, maxlength: 9,
      cardInfo: {
        typeOfCard: String, required: true, ENUM[Visa, MAsterCard, American Express, other]
        cardNumber: Number, required: true
        expDate: Date, required: true
        CVV: Number, required: true
      	}
		})
          
  - RentRequest 
    new Schema ({
			_id: ,
      gameOwnerRef: user._id, 
      gameRef: gameForRent._id,
      gameRenterRef: user._id,
			days: Number, required: true, 
    })
    
  - GameForRent 
		new Schema ({
			_id: ,
			gameAPIref: API._id,
			request: [rentRequest._id,,,]
			price: Number, required: true,
			maxDays: Number, required: true
			isAvailable: Boolean, **
    })
    
    <br>
    
## Backlog

 - Confirmation.hbs
    - Summary of product
    - Confirmation button
    
 - User profile
    - Wishlist
    - Check who is renting my game in the games list
    - Who favorited the games posted
    
 - Success
    - Contact button besides the 'go home' to call the other user
    
 - Homepage
    - Filter part on the search
    
<br>

## Links
[Trello Link]


### Git
[Repository Link]

[Deploy Link]

<br>

### Slides
[Google Slides Link]
