# MongoBlogger

- getPosts

const getPosts = (searchObject, sortObject, limit, skip) => {
    const posts = db.blogs.find(searchObject).toArray()
    return posts
}

const searchObject = {
    createdAt: {
        $gt: new Date("2022-05-01")
    }
}
const sortObject = {}
const limit = 10
const skip = 0

// Uncomment the following line when you're ready to run getPosts
// const posts = getPosts(searchObject, sortObject, limit, skip)
// console.log(posts)

/* 
Requirements:
    - Update searchObject so that the query in getPosts searches for all posts with a createdAt date greater than May 1, 2022
Stretch goals: 
    - Update the code in getPosts to chain the .sort() method with the sortObject passed as an argument onto .find() so that the 
        function sorts the results. I.E. if sortObject = {lastModified: -1} then the result from getPosts should be sorted by 
        lastModified in descending order.
    - Update the code in getPosts to chain .limit() and .skip() on the results so that the search result will only return the 
        inputted limit number of posts and skip the inputted skip number of posts.
    - Update the code in getPosts so that if any of the arguments sortObject, limit and skip are undefined, the function will 
        still execute with the other arguments that are defined.
*/

- createPost

const createPost = (newPost) => {
    const id = getUUID()
    const postData = {
    title: newPost.title,
    text: newPost.text,
    author: newPost.author,
    categories: newPost.categories,
    id: id,
    createdAt: new Date(),
    lastModified: new Date(),
    objectId: 11
    }
    return db.blogs.insertOne(postData)
   
}

const newPost = {
    title: "The Dark Knight Movie Review",
    text: "This movie was amazing because I am Batman.",
    author: "Bruce Wayne",
    categories: ["superhero", "action", "thriller"],
}

// Uncomment the following line when you're ready to run createPosts
// createPost(newPost)

/*
Requirements:
    - Add code in createPost so that a new blog post will be created when createPost is called.
    Note: id, createdAt and lastModified will have to be generated. The id field can be generated with the provided getUUID() 
        function which will return a random UUID.
Stretch Goal: 
    - Add validation in createPost so that if postData does not have the required fields of title, text, author, and categories, 
        it throws an error
*/
 
 - updatePost

const updatePost = (id, newPostData) => {
    const updatedBlog = db.blogs.updateOne({
        id: id
    }, {
        $set: {
            title: newPostData.title,
            text: newPostData.text,
            author: newPostData.author,
            categories: newPostData.categories,
            id: postId,
            createdAt: newPostData.createdAt,
            lastModified: new Date(),
            objectId: 11
        }
    }) 
    return updatedBlog
}

const updatedPost = {
    title: "The Dark Knight Movie Review",
    text: "This movie was amazing because I am Batman, and totally not Bruce Wayne. I don't even know who that is.",
    author: "Batman",
    categories: ["superhero", "action", "thriller"]
}
const postId = "fb1b7a41-ca45-47b5-84f7-64f27b38249b" // This variable should be the uuid of the blog post you created before using createPost

// Uncomment the following line when you're ready to run updatePost
// updatePost(postId, updatedPost)

/*
Requirements:
    - Add code in updatePost so that Mongo will find the post created before using createPost and update it to the new data 
        in updatedPost. 
    Note: You will need to change the postId variable to be the UUID given to the blog post you created before using createPost(). 
        This value can be hardcoded in the postId variable, E.G. const postId = "fb1b7a41-ca45-47b5-84f7-64f27b38249b".
Stretch Goal:
    - Use getPosts() to find the blog post you created before and get the UUID from the id field in that blog post 
        programmatically without needing to hardcode the postId variable. 
*/

- deletePost

const deletePost = (id) => {
    const deletePost = db.blogs.deleteOne({
        id: id
    })
    return deletePost
}

const postIdToDelete = "fb1b7a41-ca45-47b5-84f7-64f27b38249b"

// Uncomment the following line when you're ready to run deletePost
deletePost(postIdToDelete)

/*
Requirements:
    - Add code in deletePost so that it will find a post by the given id and delete it.
Stretch Goal:
    - Write a new function deletePosts that takes an array of ids as an argument and deletes all of the posts with those ids.
*/