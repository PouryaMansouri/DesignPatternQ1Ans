
The identified design pattern issue in the given code is the lack of separation of concerns and violation of the Single Responsibility Principle. The ShoppingCart class is responsible for managing items, calculating discounts, and performing checkout operations. To improve the code, we can apply the Strategy design pattern.

Refactored Code:

```python
# Refactored Code with the Strategy Design Pattern

class ShoppingCart:
    def __init__(self, discount_strategy):
        self.items = []
        self.total_price = 0
        self.discount_strategy = discount_strategy

    def add_item(self, item):
        self.items.append(item)
        self.total_price += item.price

    def remove_item(self, item):
        self.items.remove(item)
        self.total_price -= item.price

    def calculate_discount(self):
        return self.discount_strategy.calculate_discount(self.total_price)

    def checkout(self):
        final_price = self.total_price - self.calculate_discount()
        print(f"Total price: {self.total_price}")
        print(f"Discount applied: {self.calculate_discount()}")
        print(f"Final price after discount: {final_price}")


class DiscountStrategy:
    def calculate_discount(self, total_price):
        pass


class RegularDiscountStrategy(DiscountStrategy):
    def calculate_discount(self, total_price):
        if total_price > 100:
            return total_price * 0.1
        else:
            return 0


class VIPDiscountStrategy(DiscountStrategy):
    def calculate_discount(self, total_price):
        return total_price * 0.2
```

Explanation:

In the refactored code, we introduced the Strategy design pattern to handle different discount calculation strategies. The ShoppingCart class now accepts a discount_strategy parameter in its constructor, allowing the flexibility to choose different discount calculation algorithms.

We defined the DiscountStrategy abstract base class that provides a common interface for all discount calculation strategies. The RegularDiscountStrategy and VIPDiscountStrategy are concrete implementations of the DiscountStrategy class, representing different discount calculation algorithms.

By utilizing the Strategy pattern, the ShoppingCart class delegates the responsibility of discount calculation to the selected strategy object. This separation of concerns adheres to the Single Responsibility Principle and makes the code more maintainable and extensible. It also enables easy addition of new discount calculation strategies in the future without modifying the existing code.

Example Usage:

```python
# Creating a ShoppingCart object with the RegularDiscountStrategy
regular_cart = ShoppingCart(RegularDiscountStrategy())
regular_cart.add_item(item1)
regular_cart.add_item(item2)
regular_cart.checkout()

# Creating a ShoppingCart object with the VIPDiscountStrategy
vip_cart = ShoppingCart(VIPDiscountStrategy())
vip_cart.add_item(item1)
vip_cart.add_item(item2)
vip_cart.checkout()
```

In this example, we demonstrate the usage of the ShoppingCart class with different discount strategies. The first ShoppingCart object uses the RegularDiscountStrategy, while the second one uses the VIPDiscountStrategy.

By applying the Strategy design pattern, the code becomes more modular, flexible, and easier to maintain.

