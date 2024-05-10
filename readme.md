 # Basic intro to Callbacks and why we need it

 when we have two functions which does some thing and one is depending on other , using callback we make sure that after function1 ,the function2 runs  ..by pasing function2 in function1 as callback ........


 # In this Example

 we have two functions 
 function createPost which makes a post
 function getPosts which takes post and show it on DOM


 when we deal with asynch JS we don't know exactly the time taken by any async task , here we mimic that situation...


 # what happens without callback

 when we invoked these two functions so what happens is that 
 here we try to mimic a network request 

 const posts = [
  { title: 'Post One', body: 'This is post one' },
  { title: 'Post Two', body: 'This is post two' },
];

function createPost(post) {
  setTimeout(() => {
    posts.push(post);
  
  }, 2000);
}

function getPosts() {
  setTimeout(() => {
    posts.forEach(function (post) {
      const div = document.createElement('div');
      div.innerHTML = `<strong>${post.title}</strong> - ${post.body}`;
      document.querySelector('#posts').appendChild(div);
    });
  }, 1000);
}

createPost({ title: 'Post Three', body: 'This is post' });
getPosts();


so what happens is that getPosts() fire off before createPosts() so on the DOM we didn't get the third post show......



# Now to overcome this issue we will make sure that  getPosts() will run after createPost()

In our script we pass a cb into createPost() where we pass our function getPosts() in and get invoked in the createPost() that way we make sure that it will run after createPost()...