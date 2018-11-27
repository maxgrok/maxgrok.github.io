---
title: "Stuck & Unstuck: Music Library CLI"
date: "2017-08-24T10:49:13.121Z"
layout: post
draft: false
path: "/posts/twenty-first-post/"
category: "Flatiron School"
tags:
  - "Ruby"
  - "Blog"
description: "This is a post about the Music Library CLI lab for Community-Based Flatiron Bootcamp."
---
The Music Library CLI Lab is a lab where one is tasked with creating  a music library that is easily accessible to search through, add songs, delete songs, and navigate through the command line interface. This is one of the final projects in the Ruby track for the Flatiron School Community-Based Bootcamp. <br><br>

Here's a breakdown of the instructions: <br><br>
1) Create an Artist, Song, and Genre class
<ul>
	<li>All classes accept a name on initialization</li>
	<li>All classes have a class variable of an array called all that is accessible via the class method .all</li>
	<li>All classes have a .destroy_all method that resets the class variable 'all' array to an empty array</li>
	<li>All classes have a custom constructor of .create</li> 
	<li>All classes have a method #save to save the instance of the class into their class variable 'all' array</li>
</ul>

2) Map Relationships Between Classes
<ul>
	<li><em>Song and Artist</em></li>
		<ul>
			<li>Songs belong to an artist.</li>
			<li>Artist has many songs.</li>
			<li>Adding songs to an artist is done by calling an #add_song method on an instance of the artist class.</li>
			<li>Songs can be initialized with an optional artist.</li>
		</ul>
	<li><em>Song and Genre</em></li>
	<li><em>Artist and Genre</em></li>
</ul>
Now, I was just stuck on the <em>Song#artist=</em> method. <br><br>
I just got unstuck by refactoring the Song#artist= method from:<br> 

```ruby
	def artist=(artist)
		#artist.name = @name
		#artist.add_song(@@all)
		self.artist.add_song(self)
	end 
```

to:
```ruby
	def artist=(artist)
		#artist.name = @name
		#artist.add_song(@@all)
		if artist == nil
			@artist = artist
		elsif artist != nil
			@artist = artist
			artist.add_song(self)
		end
	end 

```
<br>
Artist#add_song method:<br>
```ruby
def add_song(song)
		@songs.include?(song) ? @songs : @songs << song
		song.artist == nil ? song.artist = self : @songs
	end
```

The above edit accounts for what to do if artist is nil, as well as not nil. The problem I was having before is that artist.add_song(self) was not sufficient because I was not defining the artist as equal to an instance variable of @artist <em>first</em>. 




