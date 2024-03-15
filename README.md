# RETO-2
Reto 2 programación orientada a objetos

## Clase Linea

Creamos la clase linea que tiene los atributos de instancia star_x, star_y, end_x, end_y. Y otros atributos de clase que son lenght y slope. 

Del mismo modo, formamos los metodos de instancias son: __init__ para el inicializador, compute_slope() para hallar la de la pendiente, compute_horizontal_cross() para verificar si intersecta con el eje x y compute_vertical_cross() para verificar si intersecta con el eje y
``` python 
import math
#Importamos math
class Line:
  lenght : float = 0
  slope : float = 0

  def __init__(self, start_x, start_y, end_x, end_y):
      self.start_x = start_x
      self.start_y = start_y
      self.end_x = end_x
      self.end_y = end_y

  def compute_slope(self):
      rise = self.end_y - self.start_y
      run = self.end_x - self.start_x
      slope_radians = math.atan2(rise, run) #Nos permite sacar el angulo en radianes mediante el metodo arcotangente, para hacer uso del eje y y x
      slope_degrees = math.degrees(slope_radians) #Pasamos a grados
      return slope_degrees

  def compute_lenght(self):
      distance = math.sqrt((self.end_x - self.start_x)**2 + (self.end_y - self.start_y)**2 ) 
      return distance
  def compute_horizontal_cross(self):
    if self.end_y * self.start_y < 0: #If y_end is positive and y_start is negative means that the line is going upwards, and the result talks abour an attempt to show that the line interesects the x-axis
      return "The line intersects the x-axis"
    else:
      return "The line does not intersect the x-axis"
#En este caso significa que tuvo que pasar de un cuadrante negativo a uno positivo para el eje y o visceversa

  def compute_vertical_cross(self):
    if self.end_x * self.start_x < 0: #Si el producto es negativo significa que la linea tuvó que haber pasado por un cuadrante negativo para x para ir hacia uno positivo
      return "The line intersects the y-axis"
    else:
      return "The line does not intersect the y axis"
line = Line(1, 1, -32, 34)
print("Exists an intersection with x-axis: ", line.compute_horizontal_cross())
print("Exists an intersection with y-axis: ", line.compute_vertical_cross())
print("The length is", line.compute_lenght())
print("Slope in degrees:", line.compute_slope())

```
## Clase Rectangulo sin método 4:
En este ejercicio buscamos hallar el area y perimetro de un rectangulo, y junto a ello observar si un cuadrado con coordenadas previamente dadas se puede encontrar dentro del rectangulo:

``` python
class Rectangle:
  def __init__(self, method):
      self.method = method

  def method1(self, blf_x, blf_y, width, height):
      self.width = width
      self.height = height
      self.bl_x = blf_x
      self.bl_y = blf_y

  def method2(self, center_x, center_y, width, height):
      self.center_x = center_x
      self.center_y = center_y
      self.width = width
      self.height = height

  def method3(self, bl_x, bl_y, ur_x, ur_y):
      self.bl_x = bl_x
      self.bl_y = bl_y
      self.ur_x = ur_x
      self.ur_y = ur_y

  def compute_area(self):
      if self.method == 1:
          return self.width * self.height
      elif self.method == 2:
          return (self.width * self.height) / 2
      elif self.method == 3:
          return (self.ur_x - self.bl_x) * (self.ur_y - self.bl_y)

  def compute_perimeter(self):
      if self.method == 1:
          return 2 * (self.width + self.height)
      elif self.method == 2:
          return 2 * self.width + 2 * self.height
      elif self.method == 3:
          return 2 * (self.ur_x - self.bl_x) + 2 * (self.ur_y - self.bl_y)


class Square(Rectangle):
  def __init__(self, method):
      super().__init__(method)

  def compute_interference_point(self, point_x, point_y):
      if self.method == 1:
          if point_x < self.bl_x or point_x > self.bl_x + self.width or point_y < self.bl_y or point_y > self.bl_y + self.height:
              return "The point is outside the square"
          else:
              return "The point is inside the square"
      elif self.method == 2:
          if point_x < self.center_x - self.width / 2 or point_x > self.center_x + self.width / 2 or point_y < self.center_y - self.height / 2 or point_y > self.center_y + self.height / 2:
              return "The point is outside the square"
          else:
              return "The point is inside the square"
      elif self.method == 3:
          if point_x > self.bl_x and point_x < self.ur_x and point_y > self.bl_y and point_y < self.ur_y:
              return "The point is inside the square"
          else:
              return "The point is outside the square"

square = Square(3)
square.method3(0, 0, 9, 5)  
print("The area is: ", square.compute_area())
point_x = -2
point_y = 3  
result = square.compute_interference_point(point_x, point_y)

print(f"This is inside the square: {result}")

```
##Class Rectangle con método 4:
En este caso vamos a encontrar el área de un rectangulo y su perimetro, pero le vamos a añadir otro método que es el 4: 




Class Restaurante:

Diagrama: 
## ![Untitled diagram-2024-03-15-004553](https://github.com/59822/RETO-2/assets/153324848/d3395bb3-36b0-4d4e-9714-556f8d174efb)

Código:

``` python
class MenuItem:
    def __init__(self, name, price, size):
        self.name = name
        self.price = price
        self.size = size

    def calculate_total_price(self, quantity):
        total_price = self.price * quantity
        self.price = total_price
        return total_price


class Beverage(MenuItem):
    def __init__(self, name, price, size):
        super().__init__(name, price, size)


class Appetizer(MenuItem):
    def __init__(self, name, price, size):
        super().__init__(name, price, size)


class MainCourse(MenuItem):
    def __init__(self, name, price, size, meat=True):
        super().__init__(name, price, size)
        self.meat = meat


class Order:
    def __init__(self):
        self.items = []

    def add_item(self, item):
        self.items.append(item)

    def calculate_total_bill(self):
        total_bill = 0
        for item in self.items:
            total_bill += item.price
        return total_bill

    def discount(self, amount):
        prix = self.calculate_total_bill()
        prix_discount = prix * (amount/100)
        prix_final = prix - prix_discount
        return prix_final

    def get_items_with_prices(self):
        items_with_prices = "\n".join([f"{item.name}: ${item.price}" for item in self.items])
        return items_with_prices


order = Order()

jugo = Beverage(name="jugo", price=4000, size="22 oz")
total_price_jugo = jugo.calculate_total_price(10)
order.add_item(jugo)

mazorca = Appetizer("Mazorca", 3500, "grande")
mazorca.calculate_total_price(3)
order.add_item(mazorca)

mignon = MainCourse("Fillet mignon", 34600, "grande", meat=True)
mignon.calculate_total_price(2)

item1 = Beverage("Soda", 2000, "12 oz")
item2 = Appetizer("Nachos", 5000, "Regular")
item3 = MainCourse("Spaghetti", 12000, "Large", meat=False)
item4 = Beverage("Iced Tea", 1500, "16 oz")
item5 = Appetizer("Chicken Wings", 8000, "Large")
item6 = MainCourse("Grilled Salmon", 18000, "Medium", meat=True)
item7 = Beverage("Lemonade", 2500, "20 oz")

order.add_item(mignon)
order.add_item(item1)
order.add_item(item2)
order.add_item(item3)
order.add_item(item4)
order.add_item(item5)
order.add_item(item6)
order.add_item(item7)

items_with_prices = order.get_items_with_prices()
print("Items with each price:\n", items_with_prices)

total_bill = order.calculate_total_bill()
print("Total bill amount:", total_bill)

discount = order.discount(90)
print("Discounted bill amount:", discount)
```
```
