---
layout: post
title:  "Just ToDo it!"
date:   2017-01-25 19:16:56 +0000
---

While working on this project I was an amazing learning  experience  for me,
although it took me way too long to get through it but I learned a boat load of new things, and some aha! moments.

Here is a partial list of what I learned:
### 1) `validates_format_of`

I was showing off my almost finished app to a friend, and while he went through the process of creating a `user` he entered random text in the email field and it let him create an account, so that got me thinking,
is there a way to validate the email format? guess what!? there is!!
(thanks [StackOverFlow](http://stackoverflow.com/a/4776937/4001311))
here is what the code looks like:
```ruby
validates_format_of :email, :with => /\A[^@\s]+@([^@\s]+\.)+[^@\s]+\z/
```
`validates_format_of` takes an atrribute name, like `:email` and `:with` lets you user Regex to match it.
I know about `validates_presence_of` but what I  didn't  know was that there
is a way to check for email format, pretty cool stuff.

### 2) Show rack-flash error message if email format is wrong
Now that I was able to validate the email format, I wanted to show a an error massage
if a user entered a invalid email, so I added it to the
 [`user`](https://github.com/Shmuwol/Daily-Todo/blob/master/app/controllers/user_controller.rb#L13)  
`post` controller using the `user.authenticate` method, like this:
```erb
flash[:notice] = "Invalid Email!" if !user.authenticate(params[:email])
redirect to '/sign_up'
```

### 3) `has_many :through`
I was trying to create a `/tasks` route where a user can view all their tasks
from all their different lists, but the way I had the data structure set up,
a `User` has many Lists, and Lists have many tasks, so I wanted to create a
variable `@tasks` where its equal to `current_user.tasks` and I'm thinking, oh no,
now I have to redo the database and 
add a `user_id` to Tasks, and then I had the aha! moment, and I finally understood
the use of `has_many :through`, the magic of ActiveRecord creates  this association,
like this `has_many :tasks, through: :lists` and this lets me use `current_user.tasks`  

![magic](http://i.imgur.com/bTNZXvn.gif)

##### check out this app on [GitHub](https://github.com/Shmuwol/Daily-Todo) and leave a comment below
