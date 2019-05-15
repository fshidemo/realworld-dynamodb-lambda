```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-fu92t6@email.com",
    "username": "author-fu92t6",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-fu92t6@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1mdTkydDYiLCJpYXQiOjE1NTc5NTE3NzcsImV4cCI6MTU1ODEyNDU3N30.Fq1uxqpNPZKMpPdOHJ8nFEeQvx3KXcfAygwXWvIOZTs",
    "username": "author-fu92t6",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-7lrh9@email.com",
    "username": "authoress-7lrh9",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-7lrh9@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy03bHJoOSIsImlhdCI6MTU1Nzk1MTc3NywiZXhwIjoxNTU4MTI0NTc3fQ.fXmpWtz61bEd5wt2q3gPth-g3Oj8NXwOhDnl_HAnnsE",
    "username": "authoress-7lrh9",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-rnzyfx@email.com",
    "username": "non-author-rnzyfx",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-rnzyfx@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3Itcm56eWZ4IiwiaWF0IjoxNTU3OTUxNzc3LCJleHAiOjE1NTgxMjQ1Nzd9.zCqMPkDHFnM4Z1H8rB-gr72BeaCs7KDG8YROdOz7OQ8",
    "username": "non-author-rnzyfx",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-tjrnem",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951777159,
    "updatedAt": 1557951777159,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title--z2vi26",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951777211,
    "updatedAt": 1557951777211,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-tjrnem
```
```
200 OK

{
  "article": {
    "createdAt": 1557951777159,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-tjrnem",
    "updatedAt": 1557951777159,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title--z2vi26
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1557951777211,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title--z2vi26",
    "updatedAt": 1557951777211,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/dfydnm
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [dfydnm]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title--z2vi26

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1557951777211,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title--z2vi26",
    "updatedAt": 1557951777211,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title--z2vi26

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1557951777211,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title--z2vi26",
    "updatedAt": 1557951777211,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title--z2vi26

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1557951777211,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title--z2vi26",
    "updatedAt": 1557951777211,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title--z2vi26

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title--z2vi26

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title--z2vi26

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title--z2vi26

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title--z2vi26]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title--z2vi26

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-fu92t6]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-tjrnem/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1557951777159,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-tjrnem",
    "updatedAt": 1557951777159,
    "favoritedBy": [
      "non-author-rnzyfx"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-tjrnem
```
```
200 OK

{
  "article": {
    "createdAt": 1557951777159,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-tjrnem",
    "updatedAt": 1557951777159,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-tjrnem/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-tjrnem_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-tjrnem_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-tjrnem/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1557951777159,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-tjrnem",
    "updatedAt": 1557951777159,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-tjrnem
```
```
200 OK

{}
```
```
GET /articles/title-tjrnem
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-tjrnem]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title--z2vi26
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-fu92t6]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "fpfdb5",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-s46cqj",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778413,
    "updatedAt": 1557951778413,
    "author": {
      "username": "authoress-7lrh9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "fpfdb5",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "wun7y4",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-513p5g",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778452,
    "updatedAt": 1557951778452,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "wun7y4",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "8rxeg6",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-bx533a",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778488,
    "updatedAt": 1557951778488,
    "author": {
      "username": "authoress-7lrh9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8rxeg6",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "x0ldok",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-r9bit9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778524,
    "updatedAt": 1557951778524,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "x0ldok",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "soofin",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-2b3mh",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778561,
    "updatedAt": 1557951778561,
    "author": {
      "username": "authoress-7lrh9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "soofin",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "uocdva",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-whesh8",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778599,
    "updatedAt": 1557951778599,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "uocdva",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "w2nzh5",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-tvkhmr",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778639,
    "updatedAt": 1557951778639,
    "author": {
      "username": "authoress-7lrh9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "w2nzh5",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ajapz7",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-nvl3pa",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778683,
    "updatedAt": 1557951778683,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ajapz7",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "wvhk1d",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-egv9u8",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778719,
    "updatedAt": 1557951778719,
    "author": {
      "username": "authoress-7lrh9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "wvhk1d",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "udygx1",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-5dpt8",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778759,
    "updatedAt": 1557951778759,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "udygx1",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "x0e3pa",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ccgq5b",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778816,
    "updatedAt": 1557951778816,
    "author": {
      "username": "authoress-7lrh9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "x0e3pa",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "lhub1q",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-z7z3uk",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778853,
    "updatedAt": 1557951778853,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "lhub1q",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "bp58c0",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-fevwtw",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778893,
    "updatedAt": 1557951778893,
    "author": {
      "username": "authoress-7lrh9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "bp58c0",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "bl1r7t",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-jv60ar",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778927,
    "updatedAt": 1557951778927,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "bl1r7t",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "jef36v",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-w3cb6l",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951778963,
    "updatedAt": 1557951778963,
    "author": {
      "username": "authoress-7lrh9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "jef36v",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tg6odg",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-c9otmb",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951779004,
    "updatedAt": 1557951779004,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tg6odg",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "k1zc6t",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-uz106f",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951779029,
    "updatedAt": 1557951779029,
    "author": {
      "username": "authoress-7lrh9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "k1zc6t",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "81xir",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-pls8oh",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951779075,
    "updatedAt": 1557951779075,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "81xir",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "qau9cz",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-t5kuec",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951779100,
    "updatedAt": 1557951779100,
    "author": {
      "username": "authoress-7lrh9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "qau9cz",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "udopun",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-g90w13",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951779134,
    "updatedAt": 1557951779134,
    "author": {
      "username": "author-fu92t6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "udopun",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "udopun"
      ],
      "createdAt": 1557951779134,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g90w13",
      "updatedAt": 1557951779134,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qau9cz",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951779100,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t5kuec",
      "updatedAt": 1557951779100,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "81xir",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951779075,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-pls8oh",
      "updatedAt": 1557951779075,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k1zc6t",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951779029,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uz106f",
      "updatedAt": 1557951779029,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "tg6odg"
      ],
      "createdAt": 1557951779004,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c9otmb",
      "updatedAt": 1557951779004,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jef36v",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778963,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3cb6l",
      "updatedAt": 1557951778963,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bl1r7t",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778927,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jv60ar",
      "updatedAt": 1557951778927,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bp58c0",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951778893,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fevwtw",
      "updatedAt": 1557951778893,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lhub1q",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778853,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-z7z3uk",
      "updatedAt": 1557951778853,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "x0e3pa"
      ],
      "createdAt": 1557951778816,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ccgq5b",
      "updatedAt": 1557951778816,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "udygx1"
      ],
      "createdAt": 1557951778759,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5dpt8",
      "updatedAt": 1557951778759,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "wvhk1d"
      ],
      "createdAt": 1557951778719,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-egv9u8",
      "updatedAt": 1557951778719,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ajapz7",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778683,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nvl3pa",
      "updatedAt": 1557951778683,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w2nzh5"
      ],
      "createdAt": 1557951778639,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tvkhmr",
      "updatedAt": 1557951778639,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uocdva"
      ],
      "createdAt": 1557951778599,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-whesh8",
      "updatedAt": 1557951778599,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "soofin",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778561,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2b3mh",
      "updatedAt": 1557951778561,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "x0ldok"
      ],
      "createdAt": 1557951778524,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-r9bit9",
      "updatedAt": 1557951778524,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8rxeg6",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778488,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bx533a",
      "updatedAt": 1557951778488,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "wun7y4"
      ],
      "createdAt": 1557951778452,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-513p5g",
      "updatedAt": 1557951778452,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fpfdb5",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951778413,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s46cqj",
      "updatedAt": 1557951778413,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "ajapz7",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778683,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nvl3pa",
      "updatedAt": 1557951778683,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "81xir",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951779075,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-pls8oh",
      "updatedAt": 1557951779075,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jef36v",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778963,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3cb6l",
      "updatedAt": 1557951778963,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lhub1q",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778853,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-z7z3uk",
      "updatedAt": 1557951778853,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "wvhk1d"
      ],
      "createdAt": 1557951778719,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-egv9u8",
      "updatedAt": 1557951778719,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uocdva"
      ],
      "createdAt": 1557951778599,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-whesh8",
      "updatedAt": 1557951778599,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8rxeg6",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778488,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bx533a",
      "updatedAt": 1557951778488,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-7lrh9
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "qau9cz",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951779100,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t5kuec",
      "updatedAt": 1557951779100,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k1zc6t",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951779029,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uz106f",
      "updatedAt": 1557951779029,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jef36v",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778963,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3cb6l",
      "updatedAt": 1557951778963,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bp58c0",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951778893,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fevwtw",
      "updatedAt": 1557951778893,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "x0e3pa"
      ],
      "createdAt": 1557951778816,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ccgq5b",
      "updatedAt": 1557951778816,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "wvhk1d"
      ],
      "createdAt": 1557951778719,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-egv9u8",
      "updatedAt": 1557951778719,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w2nzh5"
      ],
      "createdAt": 1557951778639,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tvkhmr",
      "updatedAt": 1557951778639,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "soofin",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778561,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2b3mh",
      "updatedAt": 1557951778561,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8rxeg6",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778488,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bx533a",
      "updatedAt": 1557951778488,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fpfdb5",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951778413,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s46cqj",
      "updatedAt": 1557951778413,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-rnzyfx
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-fu92t6&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "udopun"
      ],
      "createdAt": 1557951779134,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g90w13",
      "updatedAt": 1557951779134,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "81xir",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951779075,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-pls8oh",
      "updatedAt": 1557951779075,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-fu92t6&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "tg6odg"
      ],
      "createdAt": 1557951779004,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c9otmb",
      "updatedAt": 1557951779004,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bl1r7t",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778927,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jv60ar",
      "updatedAt": 1557951778927,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "udopun"
      ],
      "createdAt": 1557951779134,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g90w13",
      "updatedAt": 1557951779134,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qau9cz",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951779100,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t5kuec",
      "updatedAt": 1557951779100,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "81xir",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951779075,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-pls8oh",
      "updatedAt": 1557951779075,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k1zc6t",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951779029,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uz106f",
      "updatedAt": 1557951779029,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "tg6odg"
      ],
      "createdAt": 1557951779004,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c9otmb",
      "updatedAt": 1557951779004,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jef36v",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778963,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3cb6l",
      "updatedAt": 1557951778963,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bl1r7t",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778927,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jv60ar",
      "updatedAt": 1557951778927,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bp58c0",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951778893,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fevwtw",
      "updatedAt": 1557951778893,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lhub1q",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778853,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-z7z3uk",
      "updatedAt": 1557951778853,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "x0e3pa"
      ],
      "createdAt": 1557951778816,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ccgq5b",
      "updatedAt": 1557951778816,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "udygx1"
      ],
      "createdAt": 1557951778759,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5dpt8",
      "updatedAt": 1557951778759,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "wvhk1d"
      ],
      "createdAt": 1557951778719,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-egv9u8",
      "updatedAt": 1557951778719,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ajapz7",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778683,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nvl3pa",
      "updatedAt": 1557951778683,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w2nzh5"
      ],
      "createdAt": 1557951778639,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tvkhmr",
      "updatedAt": 1557951778639,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uocdva"
      ],
      "createdAt": 1557951778599,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-whesh8",
      "updatedAt": 1557951778599,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "soofin",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778561,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2b3mh",
      "updatedAt": 1557951778561,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "x0ldok"
      ],
      "createdAt": 1557951778524,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-r9bit9",
      "updatedAt": 1557951778524,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8rxeg6",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778488,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bx533a",
      "updatedAt": 1557951778488,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "wun7y4"
      ],
      "createdAt": 1557951778452,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-513p5g",
      "updatedAt": 1557951778452,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fpfdb5",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951778413,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s46cqj",
      "updatedAt": 1557951778413,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-7lrh9/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-7lrh9",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "qau9cz",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951779100,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t5kuec",
      "updatedAt": 1557951779100,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k1zc6t",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951779029,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uz106f",
      "updatedAt": 1557951779029,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jef36v",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778963,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3cb6l",
      "updatedAt": 1557951778963,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bp58c0",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951778893,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fevwtw",
      "updatedAt": 1557951778893,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "x0e3pa"
      ],
      "createdAt": 1557951778816,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ccgq5b",
      "updatedAt": 1557951778816,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "wvhk1d"
      ],
      "createdAt": 1557951778719,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-egv9u8",
      "updatedAt": 1557951778719,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w2nzh5"
      ],
      "createdAt": 1557951778639,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tvkhmr",
      "updatedAt": 1557951778639,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "soofin",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778561,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2b3mh",
      "updatedAt": 1557951778561,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8rxeg6",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778488,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bx533a",
      "updatedAt": 1557951778488,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fpfdb5",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951778413,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s46cqj",
      "updatedAt": 1557951778413,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-fu92t6/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-fu92t6",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "udopun"
      ],
      "createdAt": 1557951779134,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g90w13",
      "updatedAt": 1557951779134,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qau9cz",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951779100,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t5kuec",
      "updatedAt": 1557951779100,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "81xir",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951779075,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-pls8oh",
      "updatedAt": 1557951779075,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k1zc6t",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951779029,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-uz106f",
      "updatedAt": 1557951779029,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "tg6odg"
      ],
      "createdAt": 1557951779004,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c9otmb",
      "updatedAt": 1557951779004,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jef36v",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778963,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-w3cb6l",
      "updatedAt": 1557951778963,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bl1r7t",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778927,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-jv60ar",
      "updatedAt": 1557951778927,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "bp58c0",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951778893,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fevwtw",
      "updatedAt": 1557951778893,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "lhub1q",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778853,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-z7z3uk",
      "updatedAt": 1557951778853,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "x0e3pa"
      ],
      "createdAt": 1557951778816,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ccgq5b",
      "updatedAt": 1557951778816,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "udygx1"
      ],
      "createdAt": 1557951778759,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-5dpt8",
      "updatedAt": 1557951778759,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "wvhk1d"
      ],
      "createdAt": 1557951778719,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-egv9u8",
      "updatedAt": 1557951778719,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ajapz7",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778683,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-nvl3pa",
      "updatedAt": 1557951778683,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w2nzh5"
      ],
      "createdAt": 1557951778639,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tvkhmr",
      "updatedAt": 1557951778639,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "uocdva"
      ],
      "createdAt": 1557951778599,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-whesh8",
      "updatedAt": 1557951778599,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "soofin",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1557951778561,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2b3mh",
      "updatedAt": 1557951778561,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "x0ldok"
      ],
      "createdAt": 1557951778524,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-r9bit9",
      "updatedAt": 1557951778524,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8rxeg6",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1557951778488,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bx533a",
      "updatedAt": 1557951778488,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1",
        "wun7y4"
      ],
      "createdAt": 1557951778452,
      "author": {
        "username": "author-fu92t6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-513p5g",
      "updatedAt": 1557951778452,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fpfdb5",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1557951778413,
      "author": {
        "username": "authoress-7lrh9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s46cqj",
      "updatedAt": 1557951778413,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "tag_8",
    "tag_mod_2_0",
    "tag_mod_3_2",
    "wvhk1d",
    "lhub1q",
    "tag_11",
    "tag_mod_2_1",
    "81xir",
    "tag_17",
    "bl1r7t",
    "tag_13",
    "tag_mod_3_1",
    "fpfdb5",
    "tag_0",
    "tag_mod_3_0",
    "tag_9",
    "udygx1",
    "qau9cz",
    "tag_18",
    "soofin",
    "tag_4",
    "tag_15",
    "tg6odg",
    "jef36v",
    "tag_14",
    "tag_1",
    "wun7y4",
    "ajapz7",
    "tag_7",
    "tag_19",
    "udopun",
    "tag_6",
    "w2nzh5",
    "tag_5",
    "uocdva",
    "tag_a",
    "tag_b",
    "8rxeg6",
    "tag_2",
    "tag_3",
    "x0ldok",
    "k1zc6t",
    "tag_16",
    "tag_10",
    "x0e3pa",
    "bp58c0",
    "tag_12"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-murfyk@email.com",
    "username": "author-murfyk",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-murfyk@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1tdXJmeWsiLCJpYXQiOjE1NTc5NTE3ODAsImV4cCI6MTU1ODEyNDU4MH0.0u1akoeZj_bu0yyOgfuyCfWwYj8U1nHhEuARGex31Oo",
    "username": "author-murfyk",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-8lt90p@email.com",
    "username": "commenter-8lt90p",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-8lt90p@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci04bHQ5MHAiLCJpYXQiOjE1NTc5NTE3ODAsImV4cCI6MTU1ODEyNDU4MH0.dVgoQIIl5j-oCUZAmuSNPgN16Roa2A3kD3wC7bPowUE",
    "username": "commenter-8lt90p",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-au2ty6",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1557951780585,
    "updatedAt": 1557951780585,
    "author": {
      "username": "author-murfyk",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-au2ty6/comments

{
  "comment": {
    "body": "test comment xxenbx"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "66afbdd3-df2d-4532-b997-a52ff7992b2e",
    "slug": "title-au2ty6",
    "body": "test comment xxenbx",
    "createdAt": 1557951780614,
    "updatedAt": 1557951780614,
    "author": {
      "username": "commenter-8lt90p",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-au2ty6/comments

{
  "comment": {
    "body": "test comment kxiyfa"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "af773632-cbdb-499f-9b3a-4dc32230a8dd",
    "slug": "title-au2ty6",
    "body": "test comment kxiyfa",
    "createdAt": 1557951780653,
    "updatedAt": 1557951780653,
    "author": {
      "username": "commenter-8lt90p",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-au2ty6/comments

{
  "comment": {
    "body": "test comment jvlhvw"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "e4adcf19-5000-4c5c-94c3-5764552161cb",
    "slug": "title-au2ty6",
    "body": "test comment jvlhvw",
    "createdAt": 1557951780686,
    "updatedAt": 1557951780686,
    "author": {
      "username": "commenter-8lt90p",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-au2ty6/comments

{
  "comment": {
    "body": "test comment og2qon"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "dbe13216-6419-4e44-ae35-aae6ee7dad6f",
    "slug": "title-au2ty6",
    "body": "test comment og2qon",
    "createdAt": 1557951780715,
    "updatedAt": 1557951780715,
    "author": {
      "username": "commenter-8lt90p",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-au2ty6/comments

{
  "comment": {
    "body": "test comment fe3cqp"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "f77de1be-3b57-49ef-bbb9-28d7fd0f9ee8",
    "slug": "title-au2ty6",
    "body": "test comment fe3cqp",
    "createdAt": 1557951780745,
    "updatedAt": 1557951780745,
    "author": {
      "username": "commenter-8lt90p",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-au2ty6/comments

{
  "comment": {
    "body": "test comment -zb94gd"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "2d1169c9-2020-45a7-a65d-ee28dfb5690e",
    "slug": "title-au2ty6",
    "body": "test comment -zb94gd",
    "createdAt": 1557951780788,
    "updatedAt": 1557951780788,
    "author": {
      "username": "commenter-8lt90p",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-au2ty6/comments

{
  "comment": {
    "body": "test comment 9b7x24"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "92fb4f89-ad1f-4f11-a23a-f5beef5233c6",
    "slug": "title-au2ty6",
    "body": "test comment 9b7x24",
    "createdAt": 1557951780830,
    "updatedAt": 1557951780830,
    "author": {
      "username": "commenter-8lt90p",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-au2ty6/comments

{
  "comment": {
    "body": "test comment o2xu90"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "3a0931a7-e5fd-4573-9670-ccd54c629910",
    "slug": "title-au2ty6",
    "body": "test comment o2xu90",
    "createdAt": 1557951780857,
    "updatedAt": 1557951780857,
    "author": {
      "username": "commenter-8lt90p",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-au2ty6/comments

{
  "comment": {
    "body": "test comment efugvm"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "e99da4f8-ede0-4b67-9edd-41d0405e580f",
    "slug": "title-au2ty6",
    "body": "test comment efugvm",
    "createdAt": 1557951780893,
    "updatedAt": 1557951780893,
    "author": {
      "username": "commenter-8lt90p",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-au2ty6/comments

{
  "comment": {
    "body": "test comment od55rf"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "da1b917c-65ef-4f1e-aab7-ea3a76ac4b68",
    "slug": "title-au2ty6",
    "body": "test comment od55rf",
    "createdAt": 1557951780920,
    "updatedAt": 1557951780920,
    "author": {
      "username": "commenter-8lt90p",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-au2ty6/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-au2ty6/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment n9eya"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-au2ty6/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1557951780653,
      "id": "af773632-cbdb-499f-9b3a-4dc32230a8dd",
      "body": "test comment kxiyfa",
      "slug": "title-au2ty6",
      "author": {
        "username": "commenter-8lt90p",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557951780653
    },
    {
      "createdAt": 1557951780614,
      "id": "66afbdd3-df2d-4532-b997-a52ff7992b2e",
      "body": "test comment xxenbx",
      "slug": "title-au2ty6",
      "author": {
        "username": "commenter-8lt90p",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557951780614
    },
    {
      "createdAt": 1557951780893,
      "id": "e99da4f8-ede0-4b67-9edd-41d0405e580f",
      "body": "test comment efugvm",
      "slug": "title-au2ty6",
      "author": {
        "username": "commenter-8lt90p",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557951780893
    },
    {
      "createdAt": 1557951780745,
      "id": "f77de1be-3b57-49ef-bbb9-28d7fd0f9ee8",
      "body": "test comment fe3cqp",
      "slug": "title-au2ty6",
      "author": {
        "username": "commenter-8lt90p",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557951780745
    },
    {
      "createdAt": 1557951780686,
      "id": "e4adcf19-5000-4c5c-94c3-5764552161cb",
      "body": "test comment jvlhvw",
      "slug": "title-au2ty6",
      "author": {
        "username": "commenter-8lt90p",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557951780686
    },
    {
      "createdAt": 1557951780857,
      "id": "3a0931a7-e5fd-4573-9670-ccd54c629910",
      "body": "test comment o2xu90",
      "slug": "title-au2ty6",
      "author": {
        "username": "commenter-8lt90p",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557951780857
    },
    {
      "createdAt": 1557951780920,
      "id": "da1b917c-65ef-4f1e-aab7-ea3a76ac4b68",
      "body": "test comment od55rf",
      "slug": "title-au2ty6",
      "author": {
        "username": "commenter-8lt90p",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557951780920
    },
    {
      "createdAt": 1557951780830,
      "id": "92fb4f89-ad1f-4f11-a23a-f5beef5233c6",
      "body": "test comment 9b7x24",
      "slug": "title-au2ty6",
      "author": {
        "username": "commenter-8lt90p",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557951780830
    },
    {
      "createdAt": 1557951780788,
      "id": "2d1169c9-2020-45a7-a65d-ee28dfb5690e",
      "body": "test comment -zb94gd",
      "slug": "title-au2ty6",
      "author": {
        "username": "commenter-8lt90p",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557951780788
    },
    {
      "createdAt": 1557951780715,
      "id": "dbe13216-6419-4e44-ae35-aae6ee7dad6f",
      "body": "test comment og2qon",
      "slug": "title-au2ty6",
      "author": {
        "username": "commenter-8lt90p",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1557951780715
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-au2ty6/comments/66afbdd3-df2d-4532-b997-a52ff7992b2e
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-au2ty6/comments/af773632-cbdb-499f-9b3a-4dc32230a8dd
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-8lt90p]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-au2ty6/comments/af773632-cbdb-499f-9b3a-4dc32230a8dd
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-au2ty6/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.v31q1c1bwr@email.com",
    "username": "user1-0.v31q1c1bwr",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.v31q1c1bwr@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudjMxcTFjMWJ3ciIsImlhdCI6MTU1Nzk1MTc4MSwiZXhwIjoxNTU4MTI0NTgxfQ.WNCopY34pDCt2z2OhqAe7qHR5VzQApQPIieD_EIlOUY",
    "username": "user1-0.v31q1c1bwr",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.v31q1c1bwr@email.com",
    "username": "user1-0.v31q1c1bwr",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.v31q1c1bwr]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.v31q1c1bwr@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.v31q1c1bwr@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.v31q1c1bwr@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.v31q1c1bwr@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudjMxcTFjMWJ3ciIsImlhdCI6MTU1Nzk1MTc4MSwiZXhwIjoxNTU4MTI0NTgxfQ.WNCopY34pDCt2z2OhqAe7qHR5VzQApQPIieD_EIlOUY",
    "username": "user1-0.v31q1c1bwr",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.rjvx5k7rm4",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.rjvx5k7rm4]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.v31q1c1bwr@email.com",
    "password": "0.agl6vjnd2qm"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.v31q1c1bwr@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudjMxcTFjMWJ3ciIsImlhdCI6MTU1Nzk1MTc4MSwiZXhwIjoxNTU4MTI0NTgxfQ.WNCopY34pDCt2z2OhqAe7qHR5VzQApQPIieD_EIlOUY",
    "username": "user1-0.v31q1c1bwr",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.v31q1c1bwr
```
```
200 OK

{
  "profile": {
    "username": "user1-0.v31q1c1bwr",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.83tllzffbqm
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.83tllzffbqm]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1NTc5NTE3ODEsImV4cCI6MTU1ODEyNDU4MX0.efXMFFnIJZWzETW8tRrCoc5lP_Y783kSM8Fnp-ZL3IM",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.duzziozvajl",
    "email": "user2-0.duzziozvajl@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.duzziozvajl@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuZHV6emlvenZhamwiLCJpYXQiOjE1NTc5NTE3ODEsImV4cCI6MTU1ODEyNDU4MX0.Lvo-i8WUR1MyCL0ODhtNwuT4SJpOLkvdp56_hE_6WJA",
    "username": "user2-0.duzziozvajl",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.v31q1c1bwr@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.v31q1c1bwr",
    "email": "updated-user1-0.v31q1c1bwr@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudjMxcTFjMWJ3ciIsImlhdCI6MTU1Nzk1MTc4MSwiZXhwIjoxNTU4MTI0NTgxfQ.WNCopY34pDCt2z2OhqAe7qHR5VzQApQPIieD_EIlOUY"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.v31q1c1bwr",
    "email": "updated-user1-0.v31q1c1bwr@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudjMxcTFjMWJ3ciIsImlhdCI6MTU1Nzk1MTc4MSwiZXhwIjoxNTU4MTI0NTgxfQ.WNCopY34pDCt2z2OhqAe7qHR5VzQApQPIieD_EIlOUY"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.v31q1c1bwr",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudjMxcTFjMWJ3ciIsImlhdCI6MTU1Nzk1MTc4MSwiZXhwIjoxNTU4MTI0NTgxfQ.WNCopY34pDCt2z2OhqAe7qHR5VzQApQPIieD_EIlOUY"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.v31q1c1bwr",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAudjMxcTFjMWJ3ciIsImlhdCI6MTU1Nzk1MTc4MSwiZXhwIjoxNTU4MTI0NTgxfQ.WNCopY34pDCt2z2OhqAe7qHR5VzQApQPIieD_EIlOUY"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.lv1hcq9qwwk@email.com",
    "username": "user2-0.lv1hcq9qwwk",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.lv1hcq9qwwk@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAubHYxaGNxOXF3d2siLCJpYXQiOjE1NTc5NTE3ODIsImV4cCI6MTU1ODEyNDU4Mn0.q81ichUBGpIeMEPhn4fsfJLAE2FoBnN6bm5JMyPFF18",
    "username": "user2-0.lv1hcq9qwwk",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.lv1hcq9qwwk@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.lv1hcq9qwwk@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2019-05-15T20:23:02.066Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
