```js
**MongoDB Aggregation Framework Assignment**

**Easy**

use aggregationAssignmentDB
switched to db aggregationAssignmentDB
db.createCollection("products")
{ ok: 1 }
db.products.insertMany([
  { name: "Laptop Pro", category: "Electronics", price: 1200, quantity: 10, tags: ["computer", "portable", "work"], date_added: new Date("2023-01-15T10:00:00Z"), supplier: { name: "TechGlobe", location: "USA" } },
  { name: "Wireless Mouse", category: "Electronics", price: 25, quantity: 100, tags: ["peripheral", "computer", "wireless"], date_added: new Date("2023-02-01T11:30:00Z"), supplier: { name: "GadgetPro", location: "China" } },
  { name: "Mechanical Keyboard", category: "Electronics", price: 75, quantity: 50, tags: ["peripheral", "computer", "mechanical"], date_added: new Date("2023-01-20T14:00:00Z"), supplier: { name: "TechGlobe", location: "USA" } },
  { name: "Cotton T-Shirt", category: "Apparel", price: 20, quantity: 200, tags: ["clothing", "cotton", "casual"], date_added: new Date("2023-03-10T09:00:00Z"), supplier: { name: "FashionHub", location: "India" } },
  { name: "Denim Jeans", category: "Apparel", price: 60, quantity: 80, tags: ["clothing", "denim"], date_added: new Date("2023-03-01T16:45:00Z"), supplier: { name: "FashionHub", location: "India" } },
  { name: "Espresso Machine", category: "Home Goods", price: 250, quantity: 30, tags: ["kitchen", "appliance", "coffee"], date_added: new Date("2023-02-15T08:20:00Z"), supplier: { name: "HomeBest", location: "Germany" } },
  { name: "Smartwatch", category: "Electronics", price: 199, quantity: 25, tags: ["wearable", "gadget", "portable"], date_added: new Date("2023-04-01T12:00:00Z"), supplier: { name: "GadgetPro", location: "China" } },
  { name: "Leather Wallet", category: "Accessories", price: 45, quantity: 120, tags: ["fashion", "leather"], date_added: new Date("2023-03-20T10:10:00Z"), supplier: { name: "StyleCraft", location: "Italy" } },
  { name: "Yoga Mat", category: "Sports", price: 30, quantity: 90, tags: ["fitness", "exercise"], date_added: new Date("2023-04-05T13:00:00Z"), supplier: { name: "ActiveLife", location: "USA" } },
  { name: "Bluetooth Speaker", category: "Electronics", price: 80, quantity: 60, tags: ["audio", "portable", "wireless"], date_added: new Date("2023-02-25T17:00:00Z"), supplier: { name: "SoundWave", location: "USA" } }
]);
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('68383cdb8c42002539abd394'),
    '1': ObjectId('68383cdb8c42002539abd395'),
    '2': ObjectId('68383cdb8c42002539abd396'),
    '3': ObjectId('68383cdb8c42002539abd397'),
    '4': ObjectId('68383cdb8c42002539abd398'),
    '5': ObjectId('68383cdb8c42002539abd399'),
    '6': ObjectId('68383cdb8c42002539abd39a'),
    '7': ObjectId('68383cdb8c42002539abd39b'),
    '8': ObjectId('68383cdb8c42002539abd39c'),
    '9': ObjectId('68383cdb8c42002539abd39d')
  }
}

**1. List All Products in the "Electronics" Category**
db.products.aggregate([
  { $match: { category: "Electronics" } }
])
{
  _id: ObjectId('68383cdb8c42002539abd394'),
  name: 'Laptop Pro',
  category: 'Electronics',
  price: 1200,
  quantity: 10,
  tags: [
    'computer',
    'portable',
    'work'
  ],
  date_added: 2023-01-15T10:00:00.000Z,
  supplier: {
    name: 'TechGlobe',
    location: 'USA'
  }
}
{
  _id: ObjectId('68383cdb8c42002539abd395'),
  name: 'Wireless Mouse',
  category: 'Electronics',
  price: 25,
  quantity: 100,
  tags: [
    'peripheral',
    'computer',
    'wireless'
  ],
  date_added: 2023-02-01T11:30:00.000Z,
  supplier: {
    name: 'GadgetPro',
    location: 'China'
  }
}
{
  _id: ObjectId('68383cdb8c42002539abd396'),
  name: 'Mechanical Keyboard',
  category: 'Electronics',
  price: 75,
  quantity: 50,
  tags: [
    'peripheral',
    'computer',
    'mechanical'
  ],
  date_added: 2023-01-20T14:00:00.000Z,
  supplier: {
    name: 'TechGlobe',
    location: 'USA'
  }
}
{
  _id: ObjectId('68383cdb8c42002539abd39a'),
  name: 'Smartwatch',
  category: 'Electronics',
  price: 199,
  quantity: 25,
  tags: [
    'wearable',
    'gadget',
    'portable'
  ],
  date_added: 2023-04-01T12:00:00.000Z,
  supplier: {
    name: 'GadgetPro',
    location: 'China'
  }
}
{
  _id: ObjectId('68383cdb8c42002539abd39d'),
  name: 'Bluetooth Speaker',
  category: 'Electronics',
  price: 80,
  quantity: 60,
  tags: [
    'audio',
    'portable',
    'wireless'
  ],
  date_added: 2023-02-25T17:00:00.000Z,
  supplier: {
    name: 'SoundWave',
    location: 'USA'
  }
}

**2. Count Products per Category**
db.products.aggregate([
  {
    $group: {
      _id: "$category",
      count: { $sum: 1 }
    }
  }
])
![image](https://github.com/user-attachments/assets/5660a77b-d413-4ded-be05-6d45fe19db29)


**3. Product Names and Prices, Sorted by Price (Descending)**
db.products.aggregate([
  {
    $project: {
      _id: 0,
      name: 1,
      price: 1
    }
  },
  {
    $sort: {
      price: -1
    }
  }
])
![image](https://github.com/user-attachments/assets/ef2b7f32-c7c6-4a39-a8f1-a24af2c2e48d)


**Medium Difficulty**

**1. Total Quantity of Products by Supplier**
db.products.aggregate([
  {
    $group: {
      _id: "$supplier.name",
      totalQuantity: { $sum: "$quantity" }
    }
  }
])
![image](https://github.com/user-attachments/assets/973420e0-2591-465d-b145-f30c46ab8226)


**2. Average Price of Products per Tag**
db.products.aggregate([
  { $unwind: "$tags" },
  {
    $group: {
      _id: "$tags",
      averagePrice: { $avg: "$price" }
    }
  },
  {
    $sort: {
      averagePrice: -1
    }
  }
])
{
  _id: 'work',
  averagePrice: 1200
}
{
  _id: 'portable',
  averagePrice: 493
}
{
  _id: 'computer',
  averagePrice: 433.3333333333333
}
{
  _id: 'coffee',
  averagePrice: 250
}
{
  _id: 'appliance',
  averagePrice: 250
}
{
  _id: 'kitchen',
  averagePrice: 250
}
{
  _id: 'gadget',
  averagePrice: 199
}
{
  _id: 'wearable',
  averagePrice: 199
}
{
  _id: 'audio',
  averagePrice: 80
}
{
  _id: 'mechanical',
  averagePrice: 75
}
{
  _id: 'denim',
  averagePrice: 60
}
{
  _id: 'wireless',
  averagePrice: 52.5
}
{
  _id: 'peripheral',
  averagePrice: 50
}
{
  _id: 'leather',
  averagePrice: 45
}
{
  _id: 'fashion',
  averagePrice: 45
}
{
  _id: 'clothing',
  averagePrice: 40
}
{
  _id: 'exercise',
  averagePrice: 30
}
{
  _id: 'fitness',
  averagePrice: 30
}
{
  _id: 'casual',
  averagePrice: 20
}
{
  _id: 'cotton',
  averagePrice: 20
}

**3. Products Added in February 2023**
db.products.aggregate([
  {
    $match: {
      date_added: {
        $gte: new Date("2023-02-01T00:00:00Z"),
        $lt: new Date("2023-03-01T00:00:00Z")
      }
    }
  },
  {
    $project: {
      _id: 0,
      name: 1,
      category: 1,
      formattedDateAdded: {
        $dateToString: { format: "%Y-%m-%d", date: "$date_added" }
      }
    }
  }
])
![image](https://github.com/user-attachments/assets/db427ea5-9916-40c7-9d72-6078914c526d)

```
