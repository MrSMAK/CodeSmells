# Code Smells
Examples of Code smells and Clean code

I am making a curated list of common code smells and their respective clean code in Swift programming language.

Before jumping into the code smells, here is an overview of common code smells:

- Bloaters
A Bloater smell represents a code element that has grown so large that it cannot be effectively handled.
- Large Class
- Long Method
- Long Parameter List
- Primitive Obsession

- Object-Orientation Abusers
An Object-Orientation Abuser smell occurs when code does not take full advantage of object-oriented design.
	- Alternative Classes with Different Interfaces
	- Refused Bequest
	- Switch Statements
	- Temporary Field

- Change Preventers
Change Preventer smells inhibit future development and modification of code.
	- Divergent Change
	- Parallel Inheritance Hierarchies
- Shotgun Surgery

-Dispensables
Dispensable smells are unnecessary code that causes clutter in your codebase.
- Data Class
- Duplicate Code
- Lazy Class
- Speculative Generality
- Dead Code

-Couplers
A Coupler smell represents high degrees of dependency between different parts of the codebase.
- Inappropriate Intimacy
- Feature Envy
- Message Chains
- Middle Man


- Other Code Smells
- Large Method
- Uncommunicative Name
- Type Embedded in Name
- Magic Numbers
- Inconsistent Names
- Excessive Use of Literals
- Cyclomatic Complexity
- Cognitive Complexity
- Spaghetti Code
- God Object
- Comments

The types of code smells can vary, but they generally include characteristics in the source code that may indicate a deeper problem. Also an important thing to note here is that these code smells are not necessarily bugs, but they can indicate weaknesses in design, slow down development, or increase the risk of bugs or failures. Identifying and addressing code smells is an important aspect of maintaining code quality and preventing technical debt.

Here are the examples of smelly code and clean code:

## Swift

### Example of Duplicate Code
#### Smelly Code
```
class FruitModel {
    var fruits: [Fruit]
    var searchedText: String?
    
    init() {
        //initialize
    }
    
    func getFruit() -> Int {
        if let text = searchedText {
            if !text.isEmpty {
                let searchedFruits = fruits.filter { code }
                return searchedFruits.count
            }
        }
        return fruits.count
    }
    
    func getFruitByIndex(_ at: Int) -> Fruit {
        if let text = searchedText {
            if !text.isEmpty {
                let searchedFruits = fruits.filter { code }
                return searchedFruits[at]
            }
        }
        return fruits[at]
    }
}
```
#### Clean Code

```
class FruitModel {
    var fruits: [Fruit]
    var searchedText: String?
    
    init() {
        //initialize
    }
    
    func getFruit() -> Int {
        return getFruits().count
    }
    
    func getFruitByIndex(_ at: Int) -> Fruit {
        return getFruits()[at]
    }
    
    private func getFruits() -> [Fruit] {
        if let text = searchedText, !text.isEmpty {
            return fruits.filter { code }
        }
        return fruits
    }
}
```

In the above example, the "Smelly Code" section demonstrates duplicate code in the getFruit() and getFruitByIndex() methods. The "Clean Code" section shows the refactored version, which extracts the duplicate code into a private method getFruits(), making the code more readable and maintainable.

### Example of Long Method
#### Smelly Code
```
func calculateTotalPrice(quantity: Int, price: Double, tax: Double) -> Double {
    let subTotal = Double(quantity) * price
    let totalTax = subTotal * tax
    return subTotal + totalTax
}
```

#### Clean code
```
func calculateTotalPrice(quantity: Int, price: Double, tax: Double) -> Double {
    return calculateSubTotal(quantity: quantity, price: price) + calculateTotalTax(subTotal: subTotal, tax: tax)
}

func calculateSubTotal(quantity: Int, price: Double) -> Double {
    return Double(quantity) * price
}

func calculateTotalTax(subTotal: Double, tax: Double) -> Double {
    return subTotal * tax
}
```

In the above example, the smelly code contains a long method that calculates the total price of an item. The clean code, however, refactors the long method into shorter methods, making the code more readable and maintainable.

### Example of Long Parameter List
#### Smelly Code
```
func createNewUser(name: String, age: Int, address: String, email: String, phone: String, username: String, password: String) {
    // Method implementation
}
```

#### Clean code
```
struct User {
    var name: String
    var age: Int
    var address: String
    var email: String
    var phone: String
    var username: String
    var password: String
}

func createNewUser(user: User) {
    // Method implementation
}
```

In the above example, the smelly code contains a long parameter list in the createNewUser method. The clean code, however, refactors the long parameter list into a single parameter of type User, making the code more readable and maintainable.

### Example of Uncommunicative Name
#### Smelly Code
```
func calculate(a: Double, b: Double, c: Double, d: Double, e: Double) -> Double {
    // Method implementation
}
```

#### Clean Code
```
func calculateTotalPrice(basePrice: Double, tax: Double, discount: Double, shippingCost: Double, additionalFees: Double) -> Double {
    // Method implementation
}
```

### Example of Type Embedded in Name
#### Smelly Code
```
var userNameString: String
func calculateTotalPriceDouble(quantityInt: Int, priceDouble: Double)
```

#### Clean Code
```
var userName: String
func calculateTotalPrice(quantity: Int, price: Double)
```

In the smelly code, the type is embedded in the variable and function names, leading to redundant and less readable code. The clean code, however, uses clear and concise names without embedding the type, leading to more maintainable and readable code.

### Example of Magic Numbers
#### Smelly Code
```
func calculateArea(radius: Double) -> Double {
    return 3.14 * radius * radius
}
```

#### Clean Code
```
let pi = 3.14
func calculateArea(radius: Double) -> Double {
    return pi * radius * radius
}
```

In the smelly code, the value of π (pi) is hard-coded as 3.14, which is a magic number. In the clean code, the magic number is replaced with a named constant pi, making the code more readable and maintainable.

### Example of Inconsistent Names
#### Smelly Code
```
func calculateTotalPrice(quantity: Int, price: Double, tax: Double) -> Double {
    let subTotal = Double(quantity) * price
    let totalTax = subTotal * tax
    return subTotal + totalTax
}
```

### Clean Code
```
func calculateTotalPrice(itemQuantity: Int, itemPrice: Double, itemTax: Double) -> Double {
    let subTotal = Double(itemQuantity) * itemPrice
    let totalTax = subTotal * itemTax
    return subTotal + totalTax
}
```

In the smelly code, the parameter names are inconsistent and do not clearly convey their purpose, making the code harder to understand and maintain. In the clean code, the parameter names are more consistent and descriptive, making the code more readable and maintainable.

### Example of Inconsistent Names
#### Smelly Code
```
struct Product {
    var name: String
    var price: Double
    var category: String
    var inStock: Bool
}
```

#### Clean Code
```
struct Product {
    var name: String
    var price: Double
    var category: String
    
    func isAvailableInStock() -> Bool {
        // Method implementation
    }
}
```
In the smelly code, the Product struct only contains data and no behavior. In the clean code, the isAvailableInStock method is added to provide behavior to the Product struct, addressing the "Data Class" code smell.

### Example of Switch Statements
#### Smelly Code
```
switch dayOfWeek {
case 1:
    print("Monday")
case 2:
    print("Tuesday")
case 3:
    print("Wednesday")
case 4:
    print("Thursday")
case 5:
    print("Friday")
case 6:
    print("Saturday")
case 7:
    print("Sunday")
default:
    break
}
```

#### Clean Code
```
let daysOfWeek = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"]
if dayOfWeek >= 1 && dayOfWeek <= 7 {
    print(daysOfWeek[dayOfWeek - 1])
}
```
In the smelly code, the switch statement is used to print the name of the day of the week based on the input number, which can be replaced with an array of strings and an if statement, making the code more readable and maintainable.

### Example of Temporary Field
#### Smelly Code
```
class ShoppingCart {
    var items: [String]
    var totalAmount: Double = 0.0
    
    init(items: [String]) {
        self.items = items
        calculateTotalAmount()
    }
    
    func calculateTotalAmount() {
        for item in items {
            let itemPrice = getItemPrice(item)
            totalAmount += itemPrice
        }
    }
    
    func getItemPrice(_ item: String) -> Double {
        // Some logic to determine the price of the item
        // For simplicity, using a fixed price in this example
        return 15.0
    }
}
```

#### Clean Code
```
class ShoppingCart {
    var items: [String]
    
    init(items: [String]) {
        self.items = items
    }
    
    func calculateTotalAmount() -> Double {
        var totalAmount: Double = 0.0
        
        for item in items {
            let itemPrice = getItemPrice(item)
            totalAmount += itemPrice
        }
        
        return totalAmount
    }
    
    func getItemPrice(_ item: String) -> Double {
        // Some logic to determine the price of the item
        // For simplicity, using a fixed price in this example
        return 15.0
    }
}
```

In the smelly code, the totalAmount is still a temporary field. The clean code version moves it into a local variable within the calculateTotalAmount method, reducing the scope and making the code cleaner.

### Example of Refused Bequest
#### Smelly Code
```
class Vehicle {
    func startEngine() {
        print("Engine started")
    }
    
    func stopEngine() {
        print("Engine stopped")
    }
    
    func accelerate() {
        print("Vehicle accelerating")
    }
    
    func brake() {
        print("Vehicle braking")
    }
}

class Bicycle: Vehicle {
    // Refusing the inherited engine-related methods
    
    override func startEngine() {
        print("Bicycles don't have engines")
    }
    
    override func stopEngine() {
        print("Bicycles don't have engines to stop")
    }
}
```

#### Clean Code
```
protocol Vehicle {
    func accelerate()
    func brake()
}

class Car: Vehicle {
    func startEngine() {
        print("Engine started")
    }
    
    func stopEngine() {
        print("Engine stopped")
    }
    
    func accelerate() {
        print("Car accelerating")
    }
    
    func brake() {
        print("Car braking")
    }
}

class Bicycle: Vehicle {
    func accelerate() {
        print("Bicycle accelerating")
    }
    
    func brake() {
        print("Bicycle braking")
    }
}
```

In smelly code, the Bicycle class inherits from Vehicle but refuses to implement the engine-related methods, providing minimal or inappropriate implementations.
However, In this cleaner version, the Vehicle protocol defines only the methods relevant to all vehicles. Both Car and Bicycle now adhere to the protocol, and each class implements the methods appropriate for its type. This avoids the Refused Bequest smell by not inheriting unnecessary methods and providing meaningful implementations for the shared behavior.

### Example of Alternative Classes with Different Interfaces
#### Smelly Code
```
class Rectangle {
    var width: Double
    var height: Double
    
    init(width: Double, height: Double) {
        self.width = width
        self.height = height
    }
    
    func calculateArea() -> Double {
        return width * height
    }
}

// Class to represent a circle
class Circle {
    var radius: Double
    
    init(radius: Double) {
        self.radius = radius
    }
    
    func calculateCircleArea() -> Double {
        return Double.pi * radius * radius
    }
}
```

#### Clean Code
```
protocol Shape {
    func calculateArea() -> Double
}

// Class to represent a rectangle
class Rectangle: Shape {
    var width: Double
    var height: Double
    
    init(width: Double, height: Double) {
        self.width = width
        self.height = height
    }
    
    func calculateArea() -> Double {
        return width * height
    }
}

// Class to represent a circle
class Circle: Shape {
    var radius: Double
    
    init(radius: Double) {
        self.radius = radius
    }
    
    func calculateArea() -> Double {
        return Double.pi * radius * radius
    }
}
```

In smelly code, Rectangle and Circle represent geometric shapes, but they have different method names for calculating their areas (calculateArea vs calculateCircleArea), leading to alternative classes with different interfaces.
However, In this cleaner version, we define a Shape protocol that both Rectangle and Circle conform to. Each class provides its implementation of the calculateArea method. This unified interface removes the code smell of having alternative classes with different interfaces, making the code more consistent and maintainable.

### Example of Divergent Change
#### Smelly Code
```
class ShoppingCartItem {
    var productName: String
    var price: Double
    
    init(productName: String, price: Double) {
        self.productName = productName
        self.price = price
    }
    
    // Method to apply a discount
    func applyDiscount(discountPercentage: Double) {
        price *= (1.0 - discountPercentage)
        print("Discount applied. New price: \(price)")
    }
    
    // Method to log the purchase
    func logPurchase() {
        print("Item purchased: \(productName) - Price: \(price)")
        // Log additional purchase-related information...
    }
}
```

#### Clean Code
```
class ShoppingCartItem {
    var productName: String
    var price: Double
    
    init(productName: String, price: Double) {
        self.productName = productName
        self.price = price
    }
    
    // Method to apply a discount
    func applyDiscount(discountPercentage: Double) {
        price *= (1.0 - discountPercentage)
        print("Discount applied. New price: \(price)")
    }
}

// Class to handle purchase logging
class PurchaseLogger {
    func logPurchase(item: ShoppingCartItem) {
        print("Item purchased: \(item.productName) - Price: \(item.price)")
        // Log additional purchase-related information...
    }
}
```
In smelly code, the ShoppingCartItem class has two responsibilities: applying a discount and logging a purchase. If changes are needed for discount-related logic or purchase logging logic, the class must be modified for different reasons, indicating a Divergent Change smell.
However, In this cleaner version, the discount application logic remains within the ShoppingCartItem class, but the purchase logging responsibility is moved to a separate class (PurchaseLogger). This separation of concerns reduces the likelihood of divergent changes and makes the code more modular and maintainable. Now, changes related to purchase logging won't affect the ShoppingCartItem class, addressing the Divergent Change smell.

### Example of Shotgun Surgery
#### Smelly Code
```
class User {
    var name: String
    var email: String
    var password: String
    
    init(name: String, email: String, password: String) {
        self.name = name
        self.email = email
        self.password = password
    }
    
    func updateName(name: String) {
        self.name = name
        // Update name in database
    }
    
    func updateEmail(email: String) {
        self.email = email
        // Update email in database
    }
    
    func updatePassword(password: String) {
        self.password = password
        // Update password in database
    }
}
```

#### Clean Code
```
class User {
    var name: String
    var email: String
    var password: String
    
    init(name: String, email: String, password: String) {
        self.name = name
        self.email = email
        self.password = password
    }
    
    func updateUserInfo(name: String? = nil, email: String? = nil, password: String? = nil) {
        if let name = name {
            self.name = name
        }
        if let email = email {
            self.email = email
        }
        if let password = password {
            self.password = password
        }
        // Update user info in database
    }
}
```

In the smelly code, the User class has separate methods for updating the name, email, and password, which can lead to shotgun surgery if changes need to be made to the database update logic. In the clean code, the updateUserInfo method is added to update all user info in one place, reducing the complexity and improving the maintainability of the code.

### Example of Parallel Inheritance Hierarchies
#### Smelly Code
```
class Vehicle {
    var make: String
    var model: String
    
    init(make: String, model: String) {
        self.make = make
        self.model = model
    }
}

class Car: Vehicle {
    var numDoors: Int
    
    init(make: String, model: String, numDoors: Int) {
        self.numDoors = numDoors
        super.init(make: make, model: model)
    }
}

class Truck: Vehicle {
    var payloadCapacity: Double
    
    init(make: String, model: String, payloadCapacity: Double) {
        self.payloadCapacity = payloadCapacity
        super.init(make: make, model: model)
    }
}
```

#### Clean Code
```
class Vehicle {
    var make: String
    var model: String
    
    init(make: String, model: String) {
        self.make = make
        self.model = model
    }
}

class Car {
    var vehicle: Vehicle
    var numDoors: Int
    
    init(vehicle: Vehicle, numDoors: Int) {
        self.vehicle = vehicle
        self.numDoors = numDoors
    }
}

class Truck {
    var vehicle: Vehicle
    var payloadCapacity: Double
    
    init(vehicle: Vehicle, payloadCapacity: Double) {
        self.vehicle = vehicle
        self.payloadCapacity = payloadCapacity
    }
}
```

In the smelly code, the Car and Truck classes inherit from the Vehicle class, leading to parallel inheritance hierarchies, which can lead to increased complexity and reduced maintainability. In the clean code, the Car and Truck classes contain a Vehicle object, reducing the complexity and improving the maintainability of the code.

### Example of Lazy Class
#### Smelly Code
```
class Logger {
    func log(message: String) {
        print("Log: \(message)")
    }
}

// Another lazy class with minimal functionality
class Validator {
    func isValidEmail(email: String) -> Bool {
        return email.contains("@")
    }
}

// Main class with the core functionality
class UserManager {
    var logger: Logger
    var validator: Validator
    
    init(logger: Logger, validator: Validator) {
        self.logger = logger
        self.validator = validator
    }
    
    func registerUser(name: String, email: String) {
        if validator.isValidEmail(email: email) {
            // Register the user
            logger.log(message: "User \(name) registered with email \(email)")
            // Additional registration logic...
        } else {
            logger.log(message: "Invalid email format")
        }
    }
}
```

#### Clean Code
```
class UserManager {
    var logger: Logger
    
    init(logger: Logger) {
        self.logger = logger
    }
    
    func registerUser(name: String, email: String) {
        if isValidEmail(email: email) {
            // Register the user
            logger.log(message: "User \(name) registered with email \(email)")
            // Additional registration logic...
        } else {
            logger.log(message: "Invalid email format")
        }
    }
    
    // Moved email validation logic here
    func isValidEmail(email: String) -> Bool {
        return email.contains("@")
    }
}
```

In the smelly code, the Logger and Validator classes are examples of lazy classes that have minimal functionality. They don't provide significant value or perform a crucial role in the system. They are added for the sake of encapsulation but contribute little to the overall design.
However, In this cleaner version, the Logger and Validator classes are removed, and their functionality is incorporated into the UserManager class. The email validation logic is moved into a method within UserManager, eliminating the need for a separate Validator class. This simplifies the codebase and eliminates the parallel lazy classes, resulting in cleaner and more maintainable code.

### Example of Speculative Generality
#### Smelly Code
```
protocol Vehicle {
    func start()
    func stop()
    func refuel()
    func fly()
}

class Car: Vehicle {
    func start() {
        // Start the car
    }
    
    func stop() {
        // Stop the car
    }
    
    func refuel() {
        // Refuel the car
    }
    
    func fly() {
        // Cars can't fly, but the method is part of the interface
    }
}
```

#### Clean Code
```
protocol Vehicle {
    func start()
    func stop()
    func refuel()
}

class Car: Vehicle {
    func start() {
        // Start the car
    }
    
    func stop() {
        // Stop the car
    }
    
    func refuel() {
        // Refuel the car
    }
}
```

In the smelly code, the fly method is included in the Vehicle protocol, even though it's not applicable to all vehicles. In the clean code, the unnecessary fly method is removed from the Vehicle protocol, leading to a more focused and maintainable design.

### Example of Message Chains
#### Smelly Code
```
let customer = Customer()
let address = customer.getAddress()
let city = address.getCity()
let state = city.getState()
let country = state.getCountry()
let name = country.getName()
```

#### Clean Code
```
let customer = Customer()
let name = customer.getAddress().getCity().getState().getCountry().getName()
```

In the smelly code, the client makes a series of calls to navigate through objects, creating a message chain and tight coupling. In the clean code, the message chain is reduced by making a single call to retrieve the desired information, leading to reduced dependency and improved code maintainability.

### Example of Middle Man
#### Smelly Code
```
class Customer {
    var name: String
    var address: Address
    
    init(name: String, address: Address) {
        self.name = name
        self.address = address
    }
    
    func getAddress() -> Address {
        return address
    }
}

class Address {
    var street: String
    var city: String
    var state: String
    
    init(street: String, city: String, state: String) {
        self.street = street
        self.city = city
        self.state = state
    }
    
    func getCity() -> String {
        return city
    }
}
```

#### Clean Code
```
class Customer {
    var name: String
    var address: Address
    
    init(name: String, address: Address) {
        self.name = name
        self.address = address
    }
}

class Address {
    var street: String
    var city: String
    var state: String
    
    init(street: String, city: String, state: String) {
        self.street = street
        self.city = city
        self.state = state
    }
}
```

In the smelly code, the Customer class has a getAddress method that returns the Address object, which can be accessed directly, leading to the middle man code smell. In the clean code, the getAddress method is removed, and the Address object is accessed directly, leading to a simpler and more maintainable design.

### Example of Inappropriate Intimacy
#### Smelly Code
```
// Class representing a customer
class Customer {
    var name: String
    var email: String
    
    init(name: String, email: String) {
        self.name = name
        self.email = email
    }
    
    // Method that has inappropriate intimacy with Order
    func placeOrder(product: String, quantity: Int) {
        let order = Order(customer: self, product: product, quantity: quantity)
        order.processOrder()
    }
}

// Class representing an order
class Order {
    var customer: Customer
    var product: String
    var quantity: Int
    
    init(customer: Customer, product: String, quantity: Int) {
        self.customer = customer
        self.product = product
        self.quantity = quantity
    }
    
    // Method that has inappropriate intimacy with Customer
    func processOrder() {
        print("Order processed for \(customer.name) - Product: \(product), Quantity: \(quantity)")
        // Additional order processing logic...
    }
}
```

#### Clean Code
```
// Class representing a customer
class Customer {
    var name: String
    var email: String
    
    init(name: String, email: String) {
        self.name = name
        self.email = email
    }
    
    // Method to place an order without inappropriate intimacy
    func placeOrder(product: String, quantity: Int) {
        OrderProcessor.processOrder(customer: self, product: product, quantity: quantity)
    }
}

// Class representing an order
class Order {
    var customer: Customer
    var product: String
    var quantity: Int
    
    init(customer: Customer, product: String, quantity: Int) {
        self.customer = customer
        self.product = product
        self.quantity = quantity
    }
}

// Order processing logic moved to a separate class
class OrderProcessor {
    class func processOrder(customer: Customer, product: String, quantity: Int) {
        let order = Order(customer: customer, product: product, quantity: quantity)
        print("Order processed for \(customer.name) - Product: \(product), Quantity: \(quantity)")
        // Additional order processing logic...
    }
}
```
In smelly code, the Customer class has inappropriate intimacy with the Order class, as it directly creates an order and calls its processOrder method. This tight coupling makes the classes dependent on each other's internal details.
However, In the cleaner version, the Customer class no longer directly creates an order or calls its method. Instead, a separate OrderProcessor class is introduced to handle order processing logic. This reduces the inappropriate intimacy between the Customer and Order classes, making the code more modular and maintainable.

### Example of Feature Envy
#### Smelly Code
```
// Class representing a ShoppingCartItem
class ShoppingCartItem {
    var name: String
    var price: Double
    var quantity: Int
    
    init(name: String, price: Double, quantity: Int) {
        self.name = name
        self.price = price
        self.quantity = quantity
    }
}

// Class representing a ShoppingCart
class ShoppingCart {
    var items: [ShoppingCartItem] = []
    
    // Method with feature envy
    func calculateTotalPrice() -> Double {
        var total: Double = 0.0
        
        for item in items {
            total += item.price * Double(item.quantity)
        }
        
        return total
    }
}
```

#### Clean Code
```
// Class representing a ShoppingCartItem
class ShoppingCartItem {
    var name: String
    var price: Double
    var quantity: Int
    
    init(name: String, price: Double, quantity: Int) {
        self.name = name
        self.price = price
        self.quantity = quantity
    }
    
    // Move the feature to its appropriate place
    func getTotalPrice() -> Double {
        return price * Double(quantity)
    }
}

// Class representing a ShoppingCart
class ShoppingCart {
    var items: [ShoppingCartItem] = []
    
    func calculateTotalPrice() -> Double {
        // Use the method from the ShoppingCartItem class
        return items.reduce(0.0) { $0 + $1.getTotalPrice() }
    }
}
```

In smelly code, the calculateTotalPrice method in the ShoppingCart class excessively uses the properties of ShoppingCartItem, indicating potential Feature Envy.
However, In this cleaner version, the getTotalPrice method is moved to the ShoppingCartItem class, eliminating the Feature Envy smell. The calculateTotalPrice method in the ShoppingCart class now uses this method from ShoppingCartItem. This makes the code more object-oriented and ensures that each class is responsible for its own behavior.

### Example of Primitive Obsession
#### Smelly Code
```
struct Employee {
    var name: String
    var id: Int
    var department: String
    var hourlyRate: Double
    // ... other properties and methods
}
```

#### Clean Code
```
struct Employee {
    var name: String
    var id: EmployeeID
    var department: Department
    var payRate: PayRate
    // ... other properties and methods
}

struct EmployeeID {
    var value: Int
    // ... other properties and methods
}

struct Department {
    var name: String
    // ... other properties and methods
}

struct PayRate {
    var amount: Double
    // ... other properties and methods
}
```

In the smelly code, the Employee struct uses primitive data types such as String, Int, and Double to represent domain concepts, leading to the primitive obsession code smell. In the clean code, domain objects such as EmployeeID, Department, and PayRate are introduced to represent these concepts, leading to a more expressive and maintainable design.

### Example of Excessive Use of Literals
#### Smelly Code
```
// Function that calculates the total price with tax
func calculateTotalPrice(price: Double) -> Double {
    let taxRate = 0.08
    let shippingCost = 5.0
    
    let totalPrice = price + (price * taxRate) + shippingCost
    return totalPrice
}

// Example usage
let productPrice = 50.0
let total = calculateTotalPrice(price: productPrice)
print("Total Price: \(total)")
```

#### Clean Code
```
// Constants for tax rate and shipping cost
let taxRate = 0.08
let shippingCost = 5.0

// Function that calculates the total price with tax
func calculateTotalPrice(price: Double) -> Double {
    let totalPrice = price + (price * taxRate) + shippingCost
    return totalPrice
}

// Example usage
let productPrice = 50.0
let total = calculateTotalPrice(price: productPrice)
print("Total Price: \(total)")
```

In smelly code, the tax rate and shipping cost are hardcoded as literals within the calculateTotalPrice function. This can make the code less maintainable and flexible, especially if these values need to be changed in multiple places.
However, In the cleaner version, the tax rate and shipping cost are defined as constants outside the function. This makes the code more readable, maintainable, and allows for easier modification of these values without modifying the function itself. Constants can be easily reused across the codebase and provide a central place to manage such values.

### Example of Cyclomatic Complexity
#### Smelly Code
```
func calculateSum(numbers: [Int]) -> Int {
    var sum = 0
    for number in numbers {
        if number % 2 == 0 {
            sum += number * 2
        } else {
            sum += number
        }
    }
    return sum
}
```

#### Clean Code
```
func calculateSum(numbers: [Int]) -> Int {
    var sum = 0
    for number in numbers {
        sum += calculateNumberSum(number: number)
    }
    return sum
}

func calculateNumberSum(number: Int) -> Int {
    if number % 2 == 0 {
        return number * 2
    } else {
        return number
    }
}
```

In the smelly code, the calculateSum function has a high cyclomatic complexity due to the if-else statement inside the for loop. In the clean code, the calculateNumberSum function is introduced to calculate the sum of each number, reducing the complexity and improving the maintainability of the code. The calculateSum function now calls the calculateNumberSum function to calculate the sum of all numbers.

### Example of Cognitive Complexity
#### Smelly Code
```
func calculateGrade(score: Int) -> String {
    if score >= 90 {
        if score == 100 {
            return "A+"
        } else {
            return "A"
        }
    } else if score >= 80 {
        return "B"
    } else if score >= 70 {
        return "C"
    } else if score >= 60 {
        return "D"
    } else {
        return "F"
    }
}
```

#### Clean Code
```
func calculateGrade(score: Int) -> String {
    if score >= 90 && score < 100 {
        return "A"
    } else if score == 100 {
        return "A+"
    } else if score >= 80 {
        return "B"
    } else if score >= 70 {
        return "C"
    } else if score >= 60 {
        return "D"
    } else {
        return "F"
    }
}
```

In the smelly code, the calculateGrade function has a high cognitive complexity due to nested if statements. In the clean code, the nested if statement is replaced with a single if statement and an additional condition, leading to a simpler and more maintainable design.

### Example of Large Class
#### Smelly Code
```
class ShoppingCart {
    var items: [String]
    var totalAmount: Double
    
    init(items: [String]) {
        self.items = items
        self.totalAmount = 0.0
    }
    
    func addItem(item: String, quantity: Int, price: Double) {
        // Add item to the shopping cart
        items.append(item)
        
        // Update the total amount
        totalAmount += Double(quantity) * price
        
        // Perform additional logic related to adding an item...
    }
    
    func removeItem(item: String, quantity: Int, price: Double) {
        // Remove item from the shopping cart
        if let index = items.firstIndex(of: item) {
            items.remove(at: index)
            
            // Update the total amount
            totalAmount -= Double(quantity) * price
            
            // Perform additional logic related to removing an item...
        }
    }
    
    func calculateTotalAmountWithTax() -> Double {
        // Calculate total amount with tax
        let taxRate = 0.08
        return totalAmount + (totalAmount * taxRate)
        
        // Perform additional logic related to tax calculation...
    }
    
    func printReceipt() {
        // Print the receipt
        print("Receipt:")
        for item in items {
            print("- \(item)")
        }
        print("Total Amount: \(calculateTotalAmountWithTax())")
        
        // Perform additional logic related to printing the receipt...
    }
    
    // Many more methods...
}
```

#### Clean Code
```
class ShoppingCart {
    var items: [String]
    
    init(items: [String]) {
        self.items = items
    }
    
    func addItem(item: String, price: Double) {
        items.append(item)
    }
    
    func removeItem(item: String) {
        if let index = items.firstIndex(of: item) {
            items.remove(at: index)
        }
    }
    
    func calculateTotalAmount() -> Double {
        return items.reduce(0.0) { $0 + $1.price }
    }
}

extension ShoppingCart {
    func calculateTotalAmountWithTax() -> Double {
        let taxRate = 0.08
        return calculateTotalAmount() + (calculateTotalAmount() * taxRate)
    }
    
    func printReceipt() {
        print("Receipt:")
        for item in items {
            print("- \(item)")
        }
        print("Total Amount: \(calculateTotalAmountWithTax())")
    }
}
```

In the smelly code, the ShoppingCart class is doing a lot: handling items, updating total amounts, calculating taxes, and printing receipts. This can make the class large, complex, and difficult to maintain.
However, in cleaner version, the responsibilities have been separated into smaller methods, and the tax calculation and receipt printing logic have been moved to an extension. The ShoppingCart class is now focused on managing items in the shopping cart, making it more readable, maintainable code.

### Example of Large Method
#### Smelly Code
```
class OrderProcessor {
    func processOrder(order: Order) {
        // Step 1: Validate order
        if !validateOrder(order) {
            print("Invalid order. Aborting processing.")
            return
        }
        
        // Step 2: Calculate total amount
        let totalAmount = calculateTotalAmount(order)
        
        // Step 3: Apply discounts
        applyDiscounts(order, totalAmount)
        
        // Step 4: Update inventory
        updateInventory(order)
        
        // Step 5: Generate invoice
        generateInvoice(order, totalAmount)
        
        // Step 6: Notify customer
        notifyCustomer(order)
    }
    
    // Many more lines of code for each step...
    
    // Helper methods for each step...
}
```

#### Clean Code
```
class OrderProcessor {
    func processOrder(order: Order) {
        if !validateOrder(order) {
            print("Invalid order. Aborting processing.")
            return
        }
        
        let totalAmount = calculateTotalAmount(order)
        applyDiscounts(order, totalAmount)
        updateInventory(order)
        generateInvoice(order, totalAmount)
        notifyCustomer(order)
    }
    
    private func validateOrder(_ order: Order) -> Bool {
        // Validation logic...
        return true
    }
    
    private func calculateTotalAmount(_ order: Order) -> Double {
        // Calculation logic...
        return 0.0
    }
    
    private func applyDiscounts(_ order: Order, _ totalAmount: Double) {
        // Discount application logic...
    }
    
    private func updateInventory(_ order: Order) {
        // Inventory update logic...
    }
    
    private func generateInvoice(_ order: Order, _ totalAmount: Double) {
        // Invoice generation logic...
    }
    
    private func notifyCustomer(_ order: Order) {
        // Customer notification logic...
    }
}
```

In smelly code, the processOrder method is doing too much, and the steps involved in processing an order are embedded within the method. This makes the method long, less readable, and harder to maintain.
However, in the cleaner version, the processOrder method is refactored into smaller private methods, each responsible for a specific step in the order processing. This makes the code more modular, readable code. Each method is focused on a specific task, making the code easier to understand and maintain thus reducing code smell.

### Example of Spaghetti Code
#### Smelly Code
```
func processOrder(order: Order) {
    if orderIsValid(order) {
        if order.paymentStatus == .pending {
            if processPayment(order) {
                if updateInventory(order) {
                    if generateInvoice(order) {
                        notifyCustomer(order)
                    } else {
                        print("Failed to generate invoice.")
                    }
                } else {
                    print("Failed to update inventory.")
                }
            } else {
                print("Payment processing failed.")
            }
        } else {
            print("Order payment is not pending.")
        }
    } else {
        print("Invalid order.")
    }
}

func orderIsValid(_ order: Order) -> Bool {
    // Validation logic...
    return true
}

func processPayment(_ order: Order) -> Bool {
    // Payment processing logic...
    return true
}

func updateInventory(_ order: Order) -> Bool {
    // Inventory update logic...
    return true
}

func generateInvoice(_ order: Order) -> Bool {
    // Invoice generation logic...
    return true
}

func notifyCustomer(_ order: Order) {
    // Customer notification logic...
}
```

#### Clean Code
```
func processOrder(order: Order) {
    guard orderIsValid(order) else {
        print("Invalid order.")
        return
    }
    
    guard order.paymentStatus == .pending else {
        print("Order payment is not pending.")
        return
    }
    
    guard processPayment(order) else {
        print("Payment processing failed.")
        return
    }
    
    guard updateInventory(order) else {
        print("Failed to update inventory.")
        return
    }
    
    guard generateInvoice(order) else {
        print("Failed to generate invoice.")
        return
    }
    
    notifyCustomer(order)
}

func orderIsValid(_ order: Order) -> Bool {
    // Validation logic...
    return true
}

func processPayment(_ order: Order) -> Bool {
    // Payment processing logic...
    return true
}

func updateInventory(_ order: Order) -> Bool {
    // Inventory update logic...
    return true
}

func generateInvoice(_ order: Order) -> Bool {
    // Invoice generation logic...
    return true
}

func notifyCustomer(_ order: Order) {
    // Customer notification logic...
}
```

In smelly code, the control flow is nested and convoluted, making it challenging to follow. This is a typical characteristic of Spaghetti Code.
However, in the cleaner version, the control flow is flattened using guard statements, making the code more readable and reducing nesting. Each step is clearly separated, and error handling is improved. This refactoring adheres to the principle of reducing complexity and making the code easier to understand and maintain.

### Example of God Object
#### Smelly Code
```
class OrderProcessingSystem {
    var orderManager: OrderManager
    var paymentProcessor: PaymentProcessor
    var inventoryManager: InventoryManager
    var invoiceGenerator: InvoiceGenerator
    var customerNotifier: CustomerNotifier
    
    init() {
        orderManager = OrderManager()
        paymentProcessor = PaymentProcessor()
        inventoryManager = InventoryManager()
        invoiceGenerator = InvoiceGenerator()
        customerNotifier = CustomerNotifier()
    }
    
    func processOrder(order: Order) {
        orderManager.processOrder(order)
        paymentProcessor.processPayment(order)
        inventoryManager.updateInventory(order)
        invoiceGenerator.generateInvoice(order)
        customerNotifier.notifyCustomer(order)
        // ... more code related to order processing
    }
    
    // ... additional methods and properties
}
```

#### Clean Code
```
class OrderProcessor {
    var orderManager: OrderManager
    var paymentProcessor: PaymentProcessor
    var inventoryManager: InventoryManager
    var invoiceGenerator: InvoiceGenerator
    var customerNotifier: CustomerNotifier
    
    init(orderManager: OrderManager,
         paymentProcessor: PaymentProcessor,
         inventoryManager: InventoryManager,
         invoiceGenerator: InvoiceGenerator,
         customerNotifier: CustomerNotifier) {
        self.orderManager = orderManager
        self.paymentProcessor = paymentProcessor
        self.inventoryManager = inventoryManager
        self.invoiceGenerator = invoiceGenerator
        self.customerNotifier = customerNotifier
    }
    
    func processOrder(order: Order) {
        orderManager.processOrder(order)
        paymentProcessor.processPayment(order)
        inventoryManager.updateInventory(order)
        invoiceGenerator.generateInvoice(order)
        customerNotifier.notifyCustomer(order)
        // ... more code related to order processing
    }
}

class OrderManager {
    func processOrder(_ order: Order) {
        // Order processing logic...
    }
}

class PaymentProcessor {
    func processPayment(_ order: Order) {
        // Payment processing logic...
    }
}

class InventoryManager {
    func updateInventory(_ order: Order) {
        // Inventory update logic...
    }
}

class InvoiceGenerator {
    func generateInvoice(_ order: Order) {
        // Invoice generation logic...
    }
}

class CustomerNotifier {
    func notifyCustomer(_ order: Order) {
        // Customer notification logic...
    }
}
```

In smelly code, the OrderProcessingSystem class is acting as a God Object, managing various aspects of order processing. This can lead to code that is difficult to maintain, test, and understand due to its broad scope of responsibilities.
However, In this cleaner version, responsibilities are separated into distinct classes (OrderManager, PaymentProcessor, InventoryManager, InvoiceGenerator, CustomerNotifier), each focusing on a specific aspect of order processing. The OrderProcessor class acts as a coordinator, orchestrating the interactions between these specialized classes.

### Example of Comments
#### Smelly Code
```
```

#### Clean Code
```
```

- Comment Your Code: Good comments should explain the "why," not the "what." They are especially useful when the code is complex or when working with others. Comments should provide insights into the rationale behind the code, its purpose, or any important considerations.
- Use Meaningful Comments: Comments should add value by providing information that is not immediately obvious from the code itself. They should help to clarify the intent of the code or explain any non-trivial implementation details.
- Avoid Redundant Comments: Redundant comments, such as those that simply restate the code in natural language, should be avoided as they can clutter the codebase and reduce its readability.

### Example of Dead Code
#### Smelly Code
```
func calculateSum(numbers: [Int]) -> Int {
    var sum = 0
    for number in numbers {
        sum += number
    }
    return sum
    print("This line of code is never executed")
}
```

#### Clean Code
```
func calculateSum(numbers: [Int]) -> Int {
    var sum = 0
    for number in numbers {
        sum += number
    }
    return sum
}
```
In the smelly code, the print statement at the end of the calculateSum function is never executed, leading to dead code. In the clean code, the dead code is removed, leading to a simpler and more maintainable design.

![Uploading image.png…]()
