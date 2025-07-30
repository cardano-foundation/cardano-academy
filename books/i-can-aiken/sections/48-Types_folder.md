# Types folder

/lib/types/arrive-on-time.ak

Still in our **Library** folder, let’s create a new subfolder for some **types** we’ll create next.

```aiken
use aiken/crypto.{VerificationKeyHash}

pub type CustomerID = VerificationKeyHash

pub type ReservationDetails {
 //unique id for the customer who made the reservation
 reserved_for: CustomerID,
 // Time after which the reservation is no longer valid
 reservation_expiry: Int,
}
```

## Explaining the code:

```aiken
use aiken/crypto.{VerificationKeyHash} 
```

This line imports the ```VerificationKeyHash``` type from the ```aiken/crypto``` module. This type represents the hash of a verification key (public key).

```aiken
pub type CustomerID = VerificationKeyHash
```

This line defines a type alias called ```CustomerID```. 

```aiken
pub type ReservationDetails {
 //unique id for the customer who made the reservation
 reserved_for: CustomerID,
 // Time after which the reservation is no longer valid
 reservation_expiry: Int,
}
```

This defines a custom type called ```ReservationDetails```. This type represents information associated with a reservation. It has two fields:

	- ```reserved_for```: A ```CustomerID``` that represents the unique identifier of the customer who made the reservation.
	- ```reservation_expiry```: An ```Int``` that represents the time ( a Unix timestamp) after which the reservation is no longer valid.

Defined with the ```type``` keyword, a custom type in Aiken is a named collection of keys and/or values. If you are familiar with object-oriented programming, custom types are like objects but with no methods. They can have named fields, or not, but you must decide one way or the other. You are not allowed a mix of named and unnamed fields. 

```aiken
// With named fields
type Datum {
	Datum { customer: ByteArray, party_size: Int }
}
// With unnamed fields
type DatumWithNoName {
	DatumWithNoName(ByteArray, Int)
}
```

Now our custom types are defined, we can use them in functions to create values by calling their constructors.

```aiken
fn bookings() {
 	let booking_1 = Datum { customer: #[0xAA, 0xBB], party_size: 8 }
 	let booking_2 = DatumWithNoName (#[0xAA, 0xBB], 2)
}
```

**Constructors**

A custom type with only one constructor and named fields can be accessed using the dot symbol (.), followed by the name of the field. For example, considering a type ```Meal```:

```aiken
type Meal {  menuName: ByteArray,  calories: Int,  rating: Int}
```

We can access any of its fields using .name, .calories and .rating respectively.

```aiken
let meal = Meal { menuName: "Waldorf Salad", calories: 500, rating: 5 }
meal.menuName // returns "Waldorf Salad"
meal.calories // returns 500
meal.rating // returns 5
 pub type Reservation {
 expiration_time: Int,
}
```

## Explaining the code:
This code defines a custom data type called ```Reservation```. Let’s take a closer look:

- ```pub type Reservation { ... }```: This declares a public type named ```Reservation```. The ```pub``` keyword means you can access and use this type from other parts of the code, or even from other modules.
- ```expiration_time: Int```: This defines a field within the ```Reservation``` type called ```expiration_time```. This field is of type ```Int```. In this context, it represents the time when the reservation expires.

This code creates a simple data structure to represent a reservation. We’ll use this later to track reservations and check if they are still valid based on their expiration time.

```aiken
use aiken/crypto.{VerificationKeyHash}
use cardano/address.{Address}

pub type CustomerID = VerificationKeyHash

pub type OrderDetails {
 customer: CustomerID,
 total_cost: Int,
}

// New type to represent the restaurant's policy, including its address

pub type RestaurantPolicy {
 restaurant_address: Address,
}
```


## Explaining the code:

Import necessary types with ‘use’ keyword. 

```use cardano/address.{Address}```: This imports the ```Address``` type.

```pub type CustomerID =  VerificationKeyHash```

This line defines a type alias called ```CustomerID```. It essentially creates a new variable, ```CustomerID```, for the ```VerificationKeyHash``` type.

```aiken
pub type OrderDetails {
 customer: CustomerID,
 total_cost: Int,
}
```

This defines a custom type called OrderDetails. This type represents information associated with a customer's order. It has two fields:

	- ```customer```: A ```CustomerID``` representing the unique identifier of the customer who placed the order.
	- ```total_cost```: An ```Int``` (integer) representing the total cost of the order in Lovelace.


```aiken
pub type RestaurantPolicy {
 restaurant_address: Address,
}
```

This defines another custom type called ```RestaurantPolicy```. This type  represents the policy of a restaurant, and, in this case, it includes a single field:

	- ```restaurant_address```: An ```Address``` representing the Cardano address of the restaurant. 

```aiken
use cardano/address.{Address}
use cardano/assets.{AssetName, PolicyId}

// Represents a specific item on the restaurant's menu

pub type MenuItem {
 policy_id: PolicyId,
 dish_name: AssetName,
}

// Represents the details of a customer's order

pub type OrderDatum {
 customer: Address,
 desired_restaurant: PolicyId,
 desired_dish: Option<AssetName>,
}
// None if any dish from the restaurant is okay
// Indicates which dish has been served to the customer

pub type ServeRedeemer {
 served_dish: MenuItem,
}

pub fn table_size() -> Int {
 // The type annotations says this returns an Int, but we don't need
 // to decide yet until we get bookings.

 todo @"wait til the phone rings with some bookings!"
}

// I want pineapple_on_pizza, otherwise fail if 'None'.

pub fn pineapple_on_pizza(opt: Option<a>) -> a {
 when opt is {
   Some(a) -> a
   None -> fail @"must have my pineapple"

 }
}
```


## Explaining the code:

```use cardano/assets.{AssetName, PolicyId}```: This imports the ```AssetName``` and ```PolicyId``` types. You can use these to represent native tokens on Cardano.
	- ```PolicyId```: A unique identifier for a token policy (the rules governing a token's minting).
	- ```AssetName```: The name of a specific token within a policy.

```aiken
// Represents a specific item on the restaurant's menu
pub type MenuItem {
 policy_id: PolicyId,
 dish_name: AssetName,
}
```

This defines a custom type called MenuItem. You can use this type to represent a specific dish on a restaurant's menu. It has two fields:
	- ```policy_id```: A ```PolicyId``` that represents the policy ID of the restaurant. 	
	- ```dish_name```: An ```AssetName``` that represents the name of the dish.


```aiken
// Represents the details of a customer's order
pub type OrderDatum {
 customer: Address,
 desired_restaurant: PolicyId,
 desired_dish: Option<AssetName>,
}
// None if any dish from the restaurant is okay
```

This defines a custom type called ```OrderDatum```. You can use this type to represent a customer's order. It has three fields:

	- ```customer```: An ```Address``` that represents the Cardano address of the customer who placed the order.
	- ```desired_restaurant```: A ```PolicyId``` that represents the policy ID of the restaurant where the customer wants to eat.
	- ```desired_dish```: An optional ```AssetName``` that represents the specific dish the customer wants to order. If this field is ```None```, it means the customer is okay with any dish from the restaurant.

```aiken
// Indicates which dish has been served to the customer

pub type ServeRedeemer {
 served_dish: MenuItem,
}
```

This defines a custom type called ```ServeRedeemer```. You can use this type to indicate which dish has been served to the customer. It has one field:

	- ```served_dish```: A ```MenuItem``` representing the dish that was served
 
This code  defines types for managing orders and menu items in a restaurant context. It uses Cardano addresses to identify customers, policy IDs to identify restaurants, and asset names to represent dishes. The ```OrderDatum``` type captures the details of a customer's order, including the desired restaurant and dish. For tracking and payment purposes, the ```ServeRedeemer``` type is used to record which dish was served to the customer.

**Option** is defined as a generic type where Option may be inhabited by any other type, so functions can use it without making assumptions on what type it is. 


```aiken
type Option<a> {  
   Some(a)  
   None
}
```

Options are used when a function must return optional values. 

## todo & fail

Aiken provides two convenient keywords, ```fail``` and ```todo```,to enable us to stop the evaluation of our program if we reach an invalid case. It also enables us to postpone some until later: a ‘to do’ at a later stage, for whatever reason.

```todo``` results in warnings at compilation to remind you of your ‘to dos’. ```fail``` will not warn you, as the compiler assumes it is a desired break point. The compiler warning hints at the expected type of the expression for your ```todo```. 

We rarely use ```String``` messages, but they can be useful for documentation, so we can add with @ “ “ notation. The string message will be traced when the ```todo``` or ```fail``` code is evaluated.

```aiken
use aiken/crypto.{VerificationKeyHash}
/// Represents a gift card with information about the owner and a secret code
pub type GiftCard {
 owner: VerificationKeyHash,
 secretCode: ByteArray,
}
```

```aiken
/// Actions that can be taken on the gift card
pub type Action {
 Cancel
 Redeem { code: ByteArray }
}
```

## Explaining the code:

This defines a custom type called ```GiftCard```. This type holds the information associated with a gift card. It has two fields:

	- ```owner```: This field is of type ```VerificationKeyHash```. This field stores the public key hash of the user who owns the gift card.
	- ```secretCode```: This field is of type ```ByteArray```. This field stores the secret code associated with the gift card, which might be required to redeem or use the gift card.

```aiken
/// Actions that can be taken on the gift card

pub type Action {
 Cancel
 Redeem { code: ByteArray }
}
```

This defines a custom type called ```Action```. You use this type to represent the different actions that can be performed on a gift card. It has two possible values:

	- ```Cancel```: This value represents the action of canceling the gift card, rendering it unusable.
	- ```Redeem { code: ByteArray }```: This value represents the action of redeeming the gift card. It includes a field code of type ```ByteArray``` that represents the secret code required for redemption. This allows the code to verify if the provided code matches the one stored in the ```GiftCard``` type.

This code sets up the necessary data types for representing a gift card and the actions that can be performed on it. It uses a public key hash to identify the owner and stores a secret code. The ```Action``` type ensures that only valid actions (canceling or redeeming) can be performed on the gift card.

```aiken
use cardano/address.{Address}

// Datum stores the essential details of an order

pub type Datum {
 restaurant: Address,
 total_cost: Int,
}
```

## Explaining the code:
```use cardano/address.{Address}```

This line imports the ```Address``` type from the ```cardano/address``` module. ```Address``` is used here to identify the restaurant associated with an order.

```aiken
// Datum stores the essential details of an order

pub type Datum {
 restaurant: Address,
 total_cost: Int,
}
```

This defines a custom type called ```Datum```. This type holds the essential information related to an order placed at a restaurant. It has two fields:

	- ```restaurant```: This field is of type ```Address```. It stores the address of the restaurant where the order was placed.
	- ```total_cost```: This field is of type ```Int``` (integer). It stores the total cost of the order, denominated in Lovelace.

This ```Datum``` type will be used in a validator later to track orders, manage payments, and ensure that funds are correctly transferred to the corresponding restaurant.

```aiken
use cardano/address.{Address}

pub type Datum {
 restaurant: Address,
 // Restaurant's address
 billAmount: Int,
}
```

## Explaining the code:

```aiken
pub type Datum {
 restaurant: Address,
 // Restaurant's address
 billAmount: Int,
}
```

This code block defines a custom data type called ```Datum```. You can use this type to store information related to a bill or invoice in a restaurant context. It has two fields:

	- ```restaurant```: This field is of type ```Address```. It stores the address of the restaurant. 
	- ```billAmount```: This field is of type ```Int```, which means it stores an integer value. This represents the total amount of the bill in Lovelace.

We’ll use this data structure later in validators to manage payments, track bills, and ensure that funds are transferred correctly.


```aiken
use aiken/crypto.{VerificationKeyHash}
/// Represents a reservation at the restaurant
pub type Reservation {
 customer: VerificationKeyHash,
 party_size: Int,
 reservation_time: Int,
}
/// Actions that can be taken on a reservation
pub type Action {
 Cancel
 Confirm { special_request: ByteArray }
}
/// Hardcoded secret phrase for special requests (now a ByteArray)
pub const secret_phrase: ByteArray = "Surprise me!"
```

## Explaining the code:
This code defines a custom type called ```Reservation``` to store information about a reservation. It has three fields:
	- ```customer```: This field is of type ```VerificationKeyHash```. 
	- ```party_size```: This field is of type ```Int``` (integer), storing the number of people in the customer's party.
	- ```reservation_time```: This field is of type ```Int``` (integer) represents the date and time of the reservation.


This code defines a custom type called ```Action``` to represent the different actions that can be performed on a reservation. It has two possible values:

	- ```Cancel```: This value represents the action of canceling the reservation.
	- ```Confirm { special_request: ByteArray }```: This value represents the action of confirming the reservation. It includes a field ```special_request``` of type ```ByteArray```, which can store an optional special request made by the customer.

```aiken
/// Hardcoded secret phrase for special requests (now a ByteArray)
pub const secret_phrase: ByteArray = "Surprise me!"
```

This line defines a constant called ```secret_phrase``` of type ```ByteArray```. This constant holds the value "Surprise me!", which is used to check for a specific special request from the customer.

This code defines data types for managing restaurant reservations. It uses a public key hash to identify customers, stores reservation details such as party size and time, and allows for actions like canceling or confirming a reservation with an optional special request. 

```aiken
use aiken/crypto.{VerificationKeyHash}
pub type OrderDatum {
 chef_hashes: List<VerificationKeyHash>,
}
```

## Explaining the code:
This defines a custom type called ```OrderDatum```. This type holds information related to an order, specifically the chefs involved in preparing the order. It has one field:
	- ```chef_hashes```: This field is of type ```List<VerificationKeyHash>```, which means it's a list of verification key hashes. An order can be associated with multiple chefs, and this field stores the hashes of their public keys to identify them.

This code defines a simple data structure to represent an order in terms of the chefs who worked on it. This ```OrderDatum``` type will be used in validators later. 

```aiken
use aiken/crypto.{VerificationKeyHash}
// Data Structure for the Tipping services
pub type Datum {
 // Restaurant owner's ID
 owner: VerificationKeyHash,
 reviews: List<ByteArray>,
}

// Actions (Redeemers)
pub type Redeemer {
 AddTip
 Claim
}
```

## Explaining the code:
This defines a custom type called ```Datum```. This type holds information related to a tipping service, specifically the owner of the service and the reviews associated with it. It has two fields:
	- ```owner```: This field is of type ```VerificationKeyHash```. It stores the public key hash of the owner of the tipping service. 
	- ```reviews```: This field is of type ```List<ByteArray>```, which means it's a list of byte arrays. The ```Datum``` can store multiple reviews, where each review is represented as a ```ByteArray```. 


```aiken
// Actions (Redeemers)

pub type Redeemer {
 AddTip
 Claim
}
```

This defines a custom type called ```Redeemer```. This type is used to represent the different actions that can be performed within the tipping service. It has two possible values:
	- ```AddTip```: This value represents the action of adding a tip, and possibly a review.
	- ```Claim```: This value represents the action of claiming the accumulated tips. The owner of the service would do this.

This code defines data types for a tipping service. It uses a public key hash to identify the service owner, stores a list of reviews as byte arrays, and defines actions for adding tips and claiming the accumulated tips.

```aiken
use aiken/crypto.{VerificationKeyHash}

// Verify membership card
//  Member details
pub type Datum {
 // Number of points needed for a reward
 required_points: Int,
 member_id_hash: MemberIDHash,
}

// Hashed membership card ID for security
pub type MemberIDHash = VerificationKeyHash

// Represents the member's total accumulated points
pub type RewardPoints = Int
```

## Explaining the code:

This defines a custom type called ```Datum```. This type holds information related to a membership card. Specifically, it holds the points required for a reward and a hashed ID for the member. It has two fields:

	- ```member_id_hash```: This field is of type ```MemberIDHash```, an alias for ```VerificationKeyHash```.
	- ```required_points```: This field is of type ```Int``` (integer). It stores the number of points required to redeem a reward. 

```aiken
// Hashed membership card ID for security
pub type MemberIDHash = VerificationKeyHash
```

This line defines a type alias called MemberIDHash. It essentially creates a new name, MemberIDHash, for the VerificationKeyHash type.

```aiken
// Represents the member's total accumulated points
pub type RewardPoints = Int
```

This line defines another type alias called ```RewardPoints```. It creates a new name for the ```Int``` type, where an integer is being used to represent the total accumulated reward points of a member.

This code defines data types for managing a membership / loyalty program. It uses a public key hash to create unique member IDs, stores the required points for rewards, and defines a type for tracking accumulated reward points.


```aiken
use aiken/crypto.{VerificationKeyHash}
pub type Datum {
 vip_id: VerificationKeyHash,
}

pub type Redeemer {
 secret_code_word: ByteArray,
}
```

## Explaining the code:
This defines a custom type called ```Datum```. This type holds information related to a VIP (Very Important Person) customer. It has one field:

 - ```vip_id```: This field is of type ```VerificationKeyHash```. It stores the public key hash of the VIP customer. 

The code defines a custom type called ```Redeemer```. This type holds a secret code word. It has one field:

- ```secret_code_word```: This field is of type ```ByteArray```.  

This code  defines two simple data types. ```Datum``` is used to identify a VIP customer using their public key hash. ```Redeemer``` is used to store a secret code word.
