## For future build

    - User is base model. User has one Donor (model to track donor info), many donations through that donor, many wishes through donations, *many animals through wishes, many toys through wishes* (skip ** unless it seems necessary to have methods for those associations)

    - Donor model is saved whenever a donation is made in order to preserve donor information regardless of account creation. Donor model belongs to user.

    - User (has registered account) has one Keeper. This model is created if the user role is set as keeper. Belongs to user.

    - Keeper has many animals, has many wishes through animals, *has many toys through wishes*

    - Animal has many wishes, has many toys through wishes

    - Admin belongs to user and is created if user role is set to admin. Can view index of everything, plus other methods for CRM stuff. (create after everything else is built)




## User Flow

    - Zookeeper

    Creates account from "For zookeepers" link on homepage (or logs in).

    When logging in, is required to create at least one animal. Also chooses toys for that
    animal at the time of creation.

    Profile page displays:
        - index of animals
        - wishes that are currently active
        - feed of actions (wishes that have been fulfilled, actions that need to be taken, etc.)
        - link for editing account
        - link for creating animals
        - link for logging out (display in header?)
        

    

## Models and Associations:

    - Donor (first name, last name, email, address: {}, )
        - has many donations
        - has many wishes through donations
        - has many animals through wishes
        - has many toys through wishes?

    - Zookeeper (good model name?)
        - belongs to zoo
        - has many animals
        - has many toys through animals

    - Admin

    - Animal
        - belongs to Zookeeper
        - belongs to Zoo
        - has many toys (or has many toys through wishes?)
        - has many donors through wishes

    - Toy
        - belongs to Animal (or belongs to Wish?)
        - belongs to Zookeeper
        - has many donors through wishes

    - Donation
        - belongs to Donor
        - belongs to wish

    - Wish (this is the object that chooses an animal and a toy, and has many donations to fund it)
        - has many donations
        - has many donors through donations
        - has one Toy
        - has one Animal

    - Zoo (probably needed?)

    - 

## Features

    - Zookeepers
        - can create new animal profiles and select toys for that animal's collection on the same form
            - checkboxes for toys 
            - cannot create new toys
        - is prompted to create at least 3 basic animal profiles and select toys for each animal on account creation
        - has full CRUD controls for animals
    
    - Donors
        - animals and toys are added to collections when creating donation
            - donation is added to "wish's" collection
        - CRUD controls only for self
        - can only view animals in own collection
        - can view donations in collection

    - Wishes
        - donations are added to collection when created by donor
        - form for donation is diplayed on front page
            - form creates new donor if no matches with email
            - when is user prompted to log in?
        - when fully funded:
            - is added to animal's collection
            - creates new Wish instance with random animal and toy attributes
                - funding overflow is transferred to new Wish's starting funding
                - donor from donation that overflowed fund amount is added to new Wish's collection
            - sends email to donors in collection



        
    
    
    
## Structures

:zoo => {   
    :name,
    :zookeepers => [{
        :name,
        :email,
        :zoo,
        :verified,
        :addresses => [{    # created by attributes hash
            :primary,
            :type,
            :business_name, 
            :street_1,
            :street_2,
            :city,
            :state,
            :zip_code,
            :country
        }],
        :animals => [{  #created by attributes hash
            :name,
            :species,
            :bio,
            :categories => []
            :wishlist => [{     # join table of toys and animals?
                :name,
                :cost,
                :vendor,
                :categories => []
            :wishes

            }],
        }],
    }]
}