# Rapid Crew - A Fashion recommandation System

Rapid Crew is built using various recommandation algorithms such as popularity based ,content based and collaborative filtering.

Popularity Based Recommender System works on the principle of popularity and or anything which is in trend. It recommends products based on Total Number of Ratings on products and average product rating given by users and fetch popular amongst them.

Content Based Recommender System works on the principle of similar content. It recommends products based on similar content of the product.The model recommands similar products to the user based on cosine similarity.

The whole Dataset Has been taken from kaggle. This dataset holds 15K records. It is a product listing from Myntra.com for the period of June 2019 to August 2019.

## Author

[Priyanshu Malaviya](https://github.com/Priyanshu9898)

## Contributing Guidelines

**Visit [Contributing.md](./Contributing.md) for contribution guidelines**

## Resources

The Dataset used in this project is taken from kaggle. It is a product listing from Myntra.com for the period of June 2019 to August 2019.
This dataset holds 15K records.

Dataset Link: [https://www.kaggle.com/datasets/promptcloud/all-products-from-myntracom-2019](https://www.kaggle.com/datasets/promptcloud/all-products-from-myntracom-2019)

## Note

**Download All Resources from here:** [https://drive.google.com/drive/folders/1GZb2v7vEoJopgDJubD3MwFCSkLFI15uq?usp=sharing](https://drive.google.com/drive/folders/1GZb2v7vEoJopgDJubD3MwFCSkLFI15uq?usp=sharing)

## Tech Stack

**Client:** React, Materil-UI, react-bootstrap

**Server:** Python, Flask

**Database:** Firebase

## Run Locally

1. Clone the project

```bash
  git clone https://github.com/Priyanshu9898/Rapid-crew
```

2.  Go to the project directory

```bash
  cd Rapid-crew
```

3.  Go to requirements.txt file in the same folder and install all required dependencies.

```bash
  npm install
```

## Environment Variables for firebase

To run this project, you will need to add the following environment variables to your firebase.js file

`API_KEY`: "AIzaSyDapzyVgu5Nv4i3s7TIw5fKFIeLS4YDB9g",

`authDomain` : "rapid-crew-1947c.firebaseapp.com",

`projectId`: "rapid-crew-1947c",

`storageBucket`: "rapid-crew-1947c.appspot.com",

`messagingSenderId`: "674640692953",

`appId`: "1:674640692953:web:c8e98832e1fa86a3ffa0c8",

`measurementId`: "G-QX9814DMG9",

4. Start the server

```bash
  npm run start
```

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

## Backend

1. Open new terminal and run

```bash
  cd Rapid-crew/backend
```

2. Create Virtual Environment in Python

```bash
  pip install virtualenv
```

```bash
  virtualenv env
```

For Windows

```bash
  .\env\Scripts\activate
```

For Mac

```bash
    source env/bin/activate
```

3. Install all python modules which are in backend/requirements.txt file

```bash
    pip install -r requirements.txt
```

4. Create .flaskenv file and add these 2 code in it

```bash
    FLASK_ENV=development
    FLASK_APP=app.py

```

Download backend_files from here: [https://drive.google.com/drive/u/0/folders/1GZb2v7vEoJopgDJubD3MwFCSkLFI15uq](https://drive.google.com/drive/u/0/folders/1GZb2v7vEoJopgDJubD3MwFCSkLFI15uq)

Add these files inside backend folder.

Folder structure may look like this:

## Screenshot

![Backend-File-structure](https://i.ibb.co/5jwH89t/backend-file-structure.png)

Run this command to start the server

```bash
    flask run
```

## API Reference

### Get 100 best selling Products- Popularity based recommendation

```bash
  GET /api/bestsellers
```

### Get BestSelling products for men- Popularity based recommendation

```bash
  GET /menProducts
```

### Get BestSelling products for women- Popularity based recommendation

```bash
  GET /womenProducts
```

### Get all products data

```bash
  GET /allProducts
```

### Get Similar Items - Content Based Recommandation

```bash
  GET /prod/${title}
```

| Parameter | Type     | Description                                                |
| :-------- | :------- | :--------------------------------------------------------- |
| `title`   | `string` | Title of the product from which fetch all similar products |

### Get Recommandation of products based on ratings- Collaborative Filtering

```bash
  GET /recommand/${title}
```

| Parameter | Type     | Description                                                                                   |
| :-------- | :------- | :-------------------------------------------------------------------------------------------- |
| `title`   | `string` | Title of the product from which fetch related products which user should buy based on ratings |

### Get the similar products available on website based on image- Fashion recommandation using Resnet model

```bash
  GET /imageData
```

### Send uploaded image data to backend for image preprocessing, feature extraction and recommandation

```bash
  POST /imageData
```

## Feature Engineering

In my myntra dataset, it has many null values available and data of columns were not suitable for training the model so for the efficient model training, feature engineering of the dataset was needed. I have created various functions for perticular column to preprocess the data.

## Popularity Based Recommandation:

As the name suggests Popularity based recommendation system works with the trend. By using ratings dataset, I found total no. of ratings on each products and average ratings of products. Then I separete products based on threshold value which I applied on totalRatings and sort products in decending order of average rating. This is how I got popular 100 products.

## Content Based Recommandation:

In this recommender system the content of the product (actual_color, dominant_color, product_type, product_details, complete_the_look, inventory, specifications etc) is used to find its similarity with other products.
I combined content of the product into one corpus by doing preprocessing on text and then apply lemmatization and remove stopwords from corpus of data using nltk (natural language processing toolkit) library.

Then by TfidfVectorizer in sklearn library, I convert my corpus of Data into vectors.

Now, I applied sigmoid_kernel through sklearn, I find the cosine similarity between products.

## Similarity score

How does it decide which item is most similar to the item user likes? Here come the similarity scores.

It is a numerical value ranges between zero to one which helps to determine how much two items are similar to each other on a scale of zero to one. This similarity score is obtained measuring the similarity between the text details of both of the items. So, similarity score is the measure of similarity between given text details of two items. This can be done by cosine-similarity.

Then the products that are most likely to be similar are recommended.

## How does Cosine Similarity Works??

![Cosine Similarity](https://i.ibb.co/HXN6mkQ/cosine-similarity.png)

The cosine similarity metric is used to determine how similar documents are regardless of their size. It estimates the cosine of the angle formed by two vectors projected in a multi-dimensional space mathematically. Because of the cosine similarity, even if two comparable documents are separated by the Euclidean distance (due to the size of the documents), they are likely to be orientated closer together. The higher the cosine similarity, the smaller the angle.

![Cosine Similarity](https://i.ibb.co/H7NWFbv/cosine-similarity2.png)

## Collaborative Filtering

Collaborative Filtering doesn???t need anything else except users??? historical preference on a set of items. Because it???s based on historical data, the core assumption here is that the users who have agreed in the past tend to also agree in the future.

Basically, the idea is to find the most similar users to your target user (nearest neighbors) and weight their ratings of an item as the prediction of the rating of this item for target user.

## Matrix Factorization

What matrix factorization eventually gives us is how much a user is aligned with a set of latent features, and how much a movie fits into this set of latent features.

![Cosine Similarity](https://i.ibb.co/ZWKP64j/cf.png)

## Product Recommandation from Image

Resnet is a pre trained image processing model. I used resnet which is a backbone of computer vision tasks to extract features from the images available in my dataset. I also extract features of uploaded image using resnet model. Then using Nearest Neighbour classifier I get the nearest similar products and show it to user.
