**MongoDB Aggregation Framework Assignment**

**Medium Difficulty**

**1. Total Quantity of Products by Supplier**
```js
db.products.aggregate([
  {
    $group: {
      _id: "$supplier.name",
      totalQuantity: { $sum: "$quantity" }
    }
  }
])
```
Output:<br>
![image](https://github.com/user-attachments/assets/973420e0-2591-465d-b145-f30c46ab8226)


**2. Average Price of Products per Tag**
```js
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
```
Output:
```js
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
```
**3. Products Added in February 2023**
```js
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
```
Output:<br>
![image](https://github.com/user-attachments/assets/db427ea5-9916-40c7-9d72-6078914c526d)

