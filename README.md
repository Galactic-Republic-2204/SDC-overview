# Backend System Desigin 

## Description

* Redesigned and scaled the backend of online retailer to handle 1M products with 10k RPS
* Designed and updated database schema for products information, product styles, products inforamtion, product photos and skus and updated tabels with indexing which improved 200% of RPS.
* Optimized PostgreSQL queries with aggregate functions and decreased queries timing to 30ms from 86ms.
* Achieved about 1000% RPS increment by identifying bottlenecks with k6 and loader.io, and horizontal scaling the backend with Nginx, catching and 3 AWS EC2 instances 

## Technologies Used
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![ExpressJS](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=%2361DAFB)
![PostGres](https://img.shields.io/badge/PostGres-000000?style=for-the-badge&logo=postgresql&logoColor=blue)
![AWS](https://img.shields.io/badge/Amazon_AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)

## Testing
Local Test: K6, chakram
Deployed: Loader.io

## Ensure that Postgresql is install onto your computer

## Installation

```
npm install
```

Start the Postgresql service on your terminal

Rename the `example.env` file to `.env` and configure the variables within.

```
npm start
```

## API Endpoints
All Queries take parameters as Query strings unless it is in the endpoint\
All responses should return status code `200 OK`

## GET Products

`/products` Retrieves the list of products

#### Parameters
| Parameter | Type    | Description                                               |
|-----------|---------|-----------------------------------------------------------|
| page      | Integer | Selects the page of results to return. Default 1.         |
| count     | Integer | Specifies how many results per page to return. Default 5.|

#### Response

```json
[{
        "product_id": 1,
        "name": "Camo Onesie",
        "description": "The So Fatigues will wake you up and fit you in. This high energy camo will have you blending in to even the wildest surroundings.",
        "category": "Jackets",
        "default_price": 140
    },
    {
        "product_id": 2,
        "name": "Bright Future Sunglasses",
        "description": "Where you're going you might not need roads, but you definitely need some shades. Give those baby blues a rest and let the future shine bright on these timeless lenses.",
        "category": "Accessories",
        "default_price": 69
    },
    {
        "product_id": 3,
        "name": "Morning Joggers",
        "description": "Whether you're a morning person or not.  Whether you're gym bound or not.  Everyone looks good in joggers.",
        "category": "Pants",
        "default_price": 40
    },
    {
        "product_id": 4,
        "name": "Slacker's Slacks",
        "description": "I'll tell you how great they are after I nap for a bit.",
        "category": "Pants",
        "default_price": 65
    },
    {
        "product_id": 5,
        "name": "Heir Force Ones",
        "description": "Now where da boxes where I keep mine? You should peep mine, maybe once or twice but never three times. I'm just a sneaker pro, I love Pumas and shell toes, but can't nothin compare to a fresh crispy white pearl",
        "category": "Kicks",
        "default_price": 99
    }
]
```

## GET Specific Product

`/products/:product_id` Returns all product level information for a specified product id.

#### Parameters
| Parameter  | Type    | Description                                       |
|------------|---------|---------------------------------------------------|
| product_id | Integer | Required ID of the Product requested |

#### Response

```json
{
    "product_id": 1,
    "name": "Camo Onesie",
    "description": "The So Fatigues will wake you up and fit you in. This high energy camo will have you blending in to even the wildest surroundings.",
    "category": "Jackets",
    "default_price": 140,
    "features": [{
        "feature": "Fabric",
        "value": "Canvas"
    }, {
        "feature": "Buttons",
        "value": "Brass"
    }]
}
```
## GET Specific Product Styles

`/products/:product_id/styles` Returns the all styles available for the given product.

#### Parameters
| Parameter  | Type    | Description                                       |
|------------|---------|---------------------------------------------------|
| product_id | Integer | Required ID of the product for which data should be returned |

```json
{
    "styles": [{
        "id": 1,
        "name": "Forest Green & Black",
        "original_price": 140,
        "default_style": true,
        "photos": [{
            "url": "https://images.unsplash.com/photo-1501088430049-71c79fa3283e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=668&q=80",
            "thumbnail_url": "https://images.unsplash.com/photo-1501088430049-71c79fa3283e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=300&q=80"
        }, {
            "url": "https://images.unsplash.com/photo-1534011546717-407bced4d25c?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2734&q=80",
            "thumbnail_url": "https://images.unsplash.com/photo-1534011546717-407bced4d25c?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=300&q=80"
        }, {
            "url": "https://images.unsplash.com/photo-1549831243-a69a0b3d39e0?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2775&q=80",
            "thumbnail_url": "https://images.unsplash.com/photo-1549831243-a69a0b3d39e0?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=300&q=80"
        }, {
            "url": "https://images.unsplash.com/photo-1527522883525-97119bfce82d?ixlib=rb-1.2.1&auto=format&fit=crop&w=668&q=80",
            "thumbnail_url": "https://images.unsplash.com/photo-1527522883525-97119bfce82d?ixlib=rb-1.2.1&auto=format&fit=crop&w=300&q=80"
        }, {
            "url": "https://images.unsplash.com/photo-1556648202-80e751c133da?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=668&q=80",
            "thumbnail_url": "https://images.unsplash.com/photo-1556648202-80e751c133da?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=300&q=80"
        }, {
            "url": "https://images.unsplash.com/photo-1532543491484-63e29b3c1f5d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1000&q=80",
            "thumbnail_url": "https://images.unsplash.com/photo-1532543491484-63e29b3c1f5d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=300&q=80"
        }],
        "skus": [{
            "id": 1,
            "size": "XS",
            "quantity": 8
        }, {
            "id": 2,
            "size": "S",
            "quantity": 16
        }, {
            "id": 3,
            "size": "M",
            "quantity": 17
        }, {
            "id": 4,
            "size": "L",
            "quantity": 10
        }, {
            "id": 5,
            "size": "XL",
            "quantity": 15
        }, {
            "id": 6,
            "size": "XL",
            "quantity": 4
        }]
    }, {
        "id": 2,
        "name": "Desert Brown & Tan",
        "original_price": 140,
        "default_style": false,
        "photos": [{
            "url": "https://images.unsplash.com/photo-1533779183510-8f55a55f15c1?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=668&q=80",
            "thumbnail_url": "https://images.unsplash.com/photo-1533779183510-8f55a55f15c1?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=300&q=80"
        }, {
            "url": "https://images.unsplash.com/photo-1560567546-4c6dbc16877b?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=668&q=80",
            "thumbnail_url": "https://images.unsplash.com/photo-1560567546-4c6dbc16877b?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=300&q=80"
        }, {
            "url": "https://images.unsplash.com/photo-1458253329476-1ebb8593a652?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80",
            "thumbnail_url": "https://images.unsplash.com/photo-1458253329476-1ebb8593a652?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=300&q=80"
        }, {
            "url": "https://images.unsplash.com/photo-1422557379185-474fa15bf770?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80",
            "thumbnail_url": "https://images.unsplash.com/photo-1422557379185-474fa15bf770?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=300&q=80"
        }, {
            "url": "https://images.unsplash.com/photo-1490723286627-4b66e6b2882a?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80",
            "thumbnail_url": "https://images.unsplash.com/photo-1490723286627-4b66e6b2882a?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=300&q=80"
        }, {
            "url": "https://images.unsplash.com/photo-1447958272669-9c562446304f?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2800&q=80",
            "thumbnail_url": "https://images.unsplash.com/photo-1447958272669-9c562446304f?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=300&q=80"
        }],
        "skus": [{
            "id": 8,
            "size": "XS",
            "quantity": 8
        }, {
            "id": 7,
            "size": "S",
            "quantity": 16
        }, {
            "id": 9,
            "size": "M",
            "quantity": 17
        }, {
            "id": 10,
            "size": "L",
            "quantity": 10
        }, {
            "id": 11,
            "size": "XL",
            "quantity": 15
        }, {
            "id": 12,
            "size": "XXL",
            "quantity": 6
        }]
    }]
}
```
## GET Related Products

`/products/:product_id/related` Returns the id's of products related to the product specified.

#### Parameters
| Parameter  | Type    | Description                                       |
|------------|---------|---------------------------------------------------|
| product_id | Integer | Required ID of the product for which data should be returned |


```json
[
	2,
	3,
	8,
	7
]
```



## Whole System Design

![Screen Shot 2022-06-23 at 8 55 39 PM](https://user-images.githubusercontent.com/78040879/175459187-cf6d19c9-6262-416e-bdfc-5dc44decc8b1.png)
