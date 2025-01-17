# 100 Days Of Code - Log


### Day 43: November 13

**Today:** Learnt about Variables and Types in Swift on Swift Playground. Started Harvard's CS50x course and listened to the week 0 computational lecture. Pset0 was in Scratch and we had to create something on it while meeting requirements. I created a chase and avoid game where a dinosaur chased white jellyfish and ate them, and had to avoid red jellyfish or they'd die. Also solved a problem with the Wordpress portfolio I'm working on where I wasn't sure how to call custom post types. 

**Thoughts:** Got frustrated with Types in Swift, understood what I was supposed to do, but just took a while to write everything down. Think I was also just excited to get started with CS50! I really enjoyed the first lecture - David Malan has a great stage presence. He made abstraction, binary code and computational thinking in general relevant and easy to understand. Scratch was a great place to start with programming, and I really enjoyed the PSet. I was inspired by a Neopets game, and felt quite empowered when I could look at a game I played as a kid and be able to decompose it and recreate it (kind of). I struggled with some of the stuff though at the end, with trying to get the game how to stop (see below). But managed to finish it and am happy with how it turned out! 

I wanted to call some CPT posts into the 404 page of the portfolio site, but was unsure how to do this at first, but got it working (see below) after searching good old Stack Overflow. 

**Learning Opportunities:** I wanted to clean up my code in Scratch, so tried to use operators to join the jellyfish objects in an if statement resulting in them either killing the dinosaur or being eaten themselves and the dinosaur scoring a point. I started with this (in pseudocode-ish):

		`if touching jellyfish1 or jellyfish2 or jellyfish3
			then win a point
			jellyfish disappears
			if score = 3 then game ends`
			

This resulted in the game ending when the first jellyfish was caught. I changed the `or` to `and`, but nothing happened (because obviouslt this meant the dino had to be touching all the jellyfish at the same time for anything to happen. I went back to the original long form where each jellyfish was under its own `if` statement. Which worked! Definitely got a firmer understanding of how literal operators can be. 

Then for calling CPTs onto a page I found this solution:

		`<?php $loop = new WP_Query( array( 'post_type' => 'custom_post_type', 'posts_per_page' => 10 ) ); ?>
				<?php while ( $loop->have_posts() ) : $loop->the_post(); ?>
						<?php the_title( '<h2 class="entry-title"><a href="' . get_permalink() . '" title="' . the_title_attribute( 'echo=0' ) . '" rel="bookmark">', '</a></h2>' ); ?>
								<div class="entry-content">
										<?php the_content(); ?>
								</div>
				<?php endwhile; ?>` 
		
Just have to edit `'custom_post_type'` to the CPT used, add `<ul></ul>` around `<?php the_title`, change `h2` to `li`, and delete `the_content` to create a ul list instead of a ‘blogroll’
    
**Link(s) to work**
_Scratch Game: An Ode to Jelly Blobs of Doom_ https://scratch.mit.edu/projects/344561054



### Day 44: November 14

**Today:** Read some articles and carried on fiddling around with the portfolio site, fixing up 404 page, footer and the header. 

**Thoughts:** Spent the day thinking about CS50, and had planned to listen to the next lecture, but was preoccupied with finishing this portfolio, as the deadline is soon. Mostly just design fiddles, working out what looked good, and how to make it accessible. 

**Learning Opportunities:** Wanted to include a gallery on the 404 page, so created a new widget sidebar just for the page. Took some fiddling to work out where to place it on the 404.php page so it floated to the right place as a sidebar and collapsed with the media queries (outside the content-area, which was obvious as soon as I looked at another page with a sidebar. Used this code which I copied from the custom widget areas in the footer: 
 
 		`<div id="error-sidebar" class="widget-area">
          <?php
            if(is_active_sidebar('error-sidebar')){
            dynamic_sidebar('error-sidebar');
            }
        	?>
			</div>'
		
Then wanted an image to replace the site title generated by WP (while still keeping the site title code there for screen readers/accessibility. Turned off 'show site title and tagline' in WP admin, and then added the following code inside the .site-branding div but outside the php loop:

	`<div id="header-image" >
	 	<a href="<?php echo esc_url( home_url( '/' ) ); ?>" title="<?php echo esc_attr( get_bloginfo( 'name', 'display' ) ); ?>" rel="home">
			<img src="<?php echo get_template_directory_uri(); ?>/inc/emilie-name.png" alt="Logo" width="HERE" height="HERE" />
		</a> 	
		</div>`

Then just fiddle with CSS. Made the mistake of giving it the same class as the site title (.site-title), which hid the image because obviously WP admin uses this class to hide the site title when needed. Thanks dev tools!

**Link(s) to work** 


### Day 45: November 15

**Today:** Played on Playgrounds, learnt about initialisation and parameters. Listened to CS50 week1 lecture on C, and got through one fo the shorts on data types too. 

**Thoughts:** Excited to get a bit further with Swift Playgrounds, I'm enjoying being able to incrementally see each skill I'm picking up, and being able to practice the older ones. Not sure what it is about this format, but it works for me. And it's so exciting to see how much more comfortable I am with the older skills already, where I don't have to think about how to use conditionals or loops. Really enjoying Swift and it's syntax, and looking forward to using it in a proper project soon. 

It's very interesting to be learning C at the same time as Swift. The format of Playgrounds is helping me understand programming syntax and how to think about things computationally, and C and the CS50 lectures give me a base of the _HOW_ Swift works and is put together. You can see C is an older language and requires so much more. Im curious to get started with the pset and see how I fare... I think I understand what's happening, but we all know that can change when I actually try _DO_. 

**Learning Opportunities:** Just some algorithm ordering in Swift that I struggled with in the exercise 'Generalizing a function'. I needed to set the parameters for the function of turning the lock up or down. I tried: 

`func turnLock (up:Bool, numberOfTimes: int)
	{
		for i in 1 ... numberOfTimes {
			if true {
				expert.turnLockUp() }
			else { 
				expert.turnLockDown() }
		}
	}`
	

That did not work. The character just kept on turning it up. Fiddled around and finally just looked it up to get an idea of where I was going wrong. Thank goodness for [Building Rainbows!](https://buildingrainbows.com)
Actually meant to be:
`func turnLock (up:Bool, numberOfTimes: int)
	{
		if up == true {
			for i in 1 ... numberOfTimes {
				expert.turnLockUp() }
		} else {
			for i in 1 ... numberOfTimes {
				expert.turnLockDown() }
		}
	}`
	
Realised I needed to determine the value of `up` before calling `for`, as my first attempt was basically just running through the `if` `else` statements a number of times, not running the command of turning the lock the number of times needed. 

**Link(s) to work** 


### Day 46: November 16

**Today:** Just finished off portfolio, had to fiddle around with final CSS stylings, getting the correct header image and cleaning up everything. Struggled with getting this live, as at first I couldn't login to the database, and after couldn't log into the wp-admin. 

**Thoughts:** I've enjoyed putting this together, especially giving more thought about how someone else will use it and how accessible it is for them to add their own stuff and edit what they need to/want to. I think when working with Wordpress one has to be more aware of how someone else might want to edit your work, eg change colours or layouts, and finding a balance between making it easy for the client, but also making sure they can't break anything. 

**Learning Opportunities:** Figured that I could create some 'custom css' in the wp-admin for the client to be able to change the feature colour. It is a yellow at the moment, but they're likely going to change that depending on what they upload. Simple as putting the specific class with styling for the colour in the custom css box under the appearance>customiser tool and leaving instructions on how to change it with the client.

No fix on getting the portfolio live. Left it for tomorrow as I was focusing on life for today. 

**Link(s) to work** Hopefully I'll be able to put this up tomorrow!


### Day 47: November 17

**Today:** Today was all about getting the portfolio live and tackling CS50s pset 1.1 (Mario less). Also got through some of w1's shorts explaining conditionals and loops in C. Really struggled with the pset and had to search around a lot for something that made it make sense to me. I'm very much a deep _how_ and _why_ thinker/understander. I need to know it all before I can accept and understand it. Took me at least 4 hours (over about 8 hours) to get it working. 

**Thoughts:** I watched the pset shorts mostly to just help with the pset. But they're really good for solidifying everything and getting some extra info. C is a weird language. Just as I think I understand it, I look at a `for` loop and get lost. Definitely needed a bit extra time to wrap my head around how the loops were written out and how they worked. I get the basics of it, and can easily do it in Swift now, but C feels clunky (for want of a better word). Totally understand why they teach it though! Once I understood it, I felt like I had a much deeper grasp of what it was doing, and felt like I could look at other languages and translate it into them (well... we'll see I guess). 

**Learning Opportunities:** 
Initially, for the Mario (Less) pset I put 
	`//loop for spaces 
		for (int sp = height - h; sp > 0; sp--)`
Instead of 
`//loop for spaces 
		for (int sp = height - h; sp > 1; sp--)`
		
which resulted in my checks failing, even though it all looked correct at first glance. When I investigated, it seemed it was printing an extra space in front of the hash, `" #"` instead of `"#"`. This is because, by having `sp > 0`, spaces were being input from row 0 (ie row 1 in CS talk), where actually one didn't want any spaces. They should've been starting from second row, which is achieved by checking the boolean expression between the two semicolons. `sp > 0` translates to "is the integer greater than 0", but because the height is starting from 1, then this is always going to be true. When I changed it to `sp > 1`, it translated to "is the integer greater than 1", so the first row (height = 1) would come back as false, and therefore no space would be printed.

To fix the portfolio I just deleted the wordpress install off the domain and literally uploaded the entire wordpress install + theme files from my localhost using Dreamhost's WebFTP. Still in the process of uploading everything... crossing fingers it works tomorrow! Definitely did something wrong somewhere along the line, but hey-ho, learning opportunity! 


**Link(s) to work:** 


### Day 48: November 18

**Today:** Played with Swift Playgrounds, and worked on getting the portfolio working. Then got ridiculously distracted looking at coding bootcamps and whether that was an option for me.  

**Thoughts:** Playgrounds is getting more interesting. Just practicing stuff slowly, but everything is becoming a lot more natural, and working out the algorithms is also coming quicker to me.   
On the coding bootcamp: I feel like I need to be immersed in code for a bit, have intentional time dedicated to learning, instead of what I'm doing at the moment, which is trying to learn what I can, but feeling like I need to be job hunting but knowing I don't have the skills (both coding or job hunting) to be ablt to get, let alone do a job yet. I'm really enjoying what I'm doing, and definitely enjoying going deeper with Swift and C than just the frontend from before (though still need to brush on ym JS). I could see myself taking on more full stack projects, or maybe even backend (with the occasional website thrown in, and obviously app design). But we'll see. It's a bit of an odd time and I can't just jump into decisions (...anymore), so will mull over it. And do an exorbitant amount of research. 

**Learning Opportunities:** Can mapping out my bootcamp options be a learning opportunity? No? Okay... I have the beginnings of a spreadsheet, but I feel like that might be a bit too much, 

**Link(s) to work** 

### Day 49: November 20

**Today:** Took a day off yesterday as I had life admin and also got stuck in coding bootcamp research. Today I got back on it, a couple levels on Playgrounds and then attempting CS50 pset1 Cash. Still trying to get the portfolio up and running.

**Thoughts:** There's so many WordPress logins... I can't keep track of them all. Playgrounds is getting fantastically more complicated. I'm working through it slowly, but really absorbing everything. Can't wait to build my first acctual Swift app!
The CS50 problem sets are deceptive. They seem liek they'll be easy, then they're ridiculously hard and you don't know where to start, and then suddenly it starts working, everything makes sense, so you submit, and then you fail and you realise you have the whole thing wrong. I love it, but also hate it, and I guess that's the point. Onwards and upwards! 

**Learning Opportunities:** Gonna be going through the problems I encounter with pset1 Cash and 'live' blog how I solve them, will hopefully retain and learn by explaining to myself as I go along:
Struggled with getting the cents to round accurately without rounding too much. As at first try input: 3.60 with `int cents = round(dollars * 100);` output: 300... which is not what I'm looking for...
Found the problem! I declared the cents as an int at the beginning, instead of float. Changed it and now it works (integers don't use decimals, so essentially the decimal was just disregarded when input). 
The hints suggested we use the modulus operator, no idea where to start with that... probably the short on operators.
- the short didn't explain much, so did some searching. Thought I'd found the way to use the modulus in this instance would be to see if the cents divided into the quarter/dime/etc without a remainder `if (cents % 25 == 0)`. That didn't work. Obviously. If I'd taken a second to do basic math I would've realised that that makes no sense... _reminder to self: dont' forget basic maths_. Then I found the walkthrough on youtube, where it was suggested we use while statements to check if 25 could be used, until it couldn't, then going doing to 10(dimes), 5(nickels) and 1 (pennies), by subtracting the coins each time without going into negatives.
	`while (cents -25 > 25) {cents - 25;}` 
After that I got it done pretty quickly!
Whoops! Came back with errors... used printf to see what the rounding was doing to the cents, but it was correct. One of the errors came back when 0.01 change was expected, fiddled aroudn and realised I needed to do `while (cents -1 >= 1) {cents - 1;}` with the equal sign. Not going to forget that one again! 

Still wasn't working... apparently the actual issue, after I took to reddit, and took a couple hours away from my screen, was incredibly obvious. `while (cents -25 >= 25)` makes no sense... at all. Apparently in my late afternoon brain it did, because if you were to write it out in pseudocode exactly it kind of would work. But not in C evidently. So quick change to `while (cents >= 25)` and everything works... _that's embarrassing_ X_X But you live and you learn!  

The walkthrough also went through the 'modular' method, so decided to give that one a go too. They didn't explain it too in-depth on the walkthrough, so I've had to go a searching for how to even start implementing it. I understand the basics of it, and that I would have to use division as well, but not even sure how to start... 
So did some reading and someone said that modular makes a lot more sense once you've given the pset1 credit a go (the more comfortable option). So will follow that advice because it seems pretty legit. 

WP Portfolio Problems: WordPress is just refusing to send me my new password for my live site. Not sure what to do... but need to get it sorted soon. 

**Link(s) to work** 

### Day 50: November 21

**Today:** Finally got the portfolio up! Sorted out admin-end stuff, ready for my client to upload their content. Played with SwiftPlaygrounds (SP)

**Thoughts:** An admin-y sort of day, but so glad I could finally get the portfolio sorted. Sometimes it's the small things (like correctly deplying a WordPress site and changing the admin password from wp-config) that make it worth it. Also seeing my client's (sister's) face when she saw the finished product and knew it was just for her - so great! 

**Learning Opportunities:** Change user name and password for wp-admin from wp-config. Already knew this deep down, but needed reminding. Also, with one-click installs, literally only move the theme folder in wp-contents. The plugins, languages and other themes etc probably don't need to be copied over most of the time (always exceptions though!). But keeping it simple is better. 

**Link(s) to work** 

### Day 51: November 22

**Today:** Squashed bugs and made slight changes in the portfolio when proper content was added. SP playing as usual.

**Thoughts:** Totally understand how important it is to walk through the finished product with the client when they're setting it up. So many random little bugs/changes...  
Also, about to move onto making worlds in SP! One step closer to feeling comfortable with Swift! 

**Learning Opportunities:**
Had some problems with the links on the images not work. Originally the code was:

	`$link = get_field('link')
	//
	<div class="card project-info">
		<a href="<?php get_field('link') ?>" target="_blank">
			<?php if($image_1) {
			echo wp_get_attachment_image( $image_1, $size );
			} ?> 
		</a>
	</div>
	`

Changed it to:

	`$url = get_field('url')
	<div class="card project-info">
		<a href="<?php echo esc_url($url); ?>"> 
			<?php if($image_2) {
			echo wp_get_attachment_image( $image_2, $size );
			} ?>
		</a>
	</div>`
	
Looked at the documentation which used `echo esc_url` instead of `get_field('link')` . Changed link to url, I'm not quite sure why this worked, but I'm guessing there was overlap with link as a variable, or url is just the better variable to use.

In CSS I had to change `.card.project-info:before ` to `.card.project-info a:after`, as the border created with the pseudo-element was 'covering' the image and its link. Added `a` to make it more specific, so the border wrapped around the link as well, instead of just the image, and `after` to push it back. 

**Link(s) to work** [Emilie's jewellery portfolio](https://emilie.beandgolden.com)

### Day 52: November 23

**Today:** SP and CS50 pset1 Credit. (Also started my application to Flatiron School... which is not really coding yet, but hopefully will be a gateway to waaaay more coding!)

**Thoughts:** Was completely stumped when I looked at the Credit pset. Literally had no idea where to start. Found the 'walkthrough' from cs50 on youtube, which reminded me about modulo (I knew it was going to come up, but wasn't sure how) and hinted as to how it would be used. Realised I knew NOTHING about modulo... 

Learnt a bit more about how I learn today instead of learning about C. I'm definitely an 'understander' before a 'doer'. I'm happy to experiment, and I'll happily try out random options, but only when I know what those random options are. Found myself too tempted to look at the answer and then work backwards, I'd rather have the information and work forwards (though both are valid ways of learning and I definitely do and will carry on using them). However, in this case, I don't want to go in completely blindly. More on this in 'learning opportunities'. 

I'm also really enjoying writing up my process while I'm going through it - makes the learning more intentional. 

**Learning Opportunitie/f%ck ups:**
The search for the meaning of modulo: tried looking for it in stack overflow specifically related to C. But it just confused me more, people kept on talking about remainders when dividing and giving examples with numbers, which when I plugged them into my calculator, made no sense. Then one lone little comment on a post pointed out: go look up modulo unrelated to programming. Duh. It's a maths term, which I knew, and I made the mistake again in my mind - went too complicated before looking at the basics. Looked up modulo, someone mentioned long division (which has long since departed my brain) so went and did a quick minute refresher trying to divide 23 by 4. 5 remainder 3. But on my calculator said 5.75. So took a step away from my desk, made a cup of tea and mulled over this conundrum and inconsistency. Duh, Sabine. .75 = 3 quarters. 3 of 4... My dumb iphone calculator doesn't have the good old option of getting remainders instead of decimals (should've stuck with my school calculator instead of Apple clearly). I's all slipped into place! SO have to get a pen and paper out and put my newly resucitated long division skills to practice.The pset requires us to access every second digit in the credit card number, starting from the second last and going backwards. The one hint they give is to use `% 10` to get to the last number. So to test how this worked I literally just wrote a random list of digits and did long divison to see how the second last number could be accessed (following the logic you'd use `% 100`). After dividing by 100, I was left with the remainder as the last 2 digits. And then it hit me. Round down and divide by 10. Got unnecessarily excited at this revelation. Onwards! 

Now I'm teaching myself arrays in C... 

3 hours later and I got distracted by videos of comedians on fb. That's usually a sign for me that I need to look at things differently. Went to see what was covered in week 2 and see arrays is coming up. So, hanging my credit hat up for a bit, as I know I learn better by properly understanding before jumping in and I'll just end up looking up the answer which I don't want to do. 

**Link(s) to work** 

### Day 53: November 23

**Today:** Started the Flatiron Bootcamp prep.

**Thoughts:** SP has definitely helped me be more comfortable with programming languages. Even though Swift and JavaScript are very different, I'm a lot less confused now that I'm looking over JavaScript again.

**Learning Opportunities:**  Learnt aabout CSS attribute selectors in the Bootcamp prep, which I think I'd definitely seen before but didn't absorb. Will probably go back into old code and see if I can update/clean up what I've written to practice. 

**Link(s) to work** 

### Day 54: November 25

**Today:** Not too much today, SP and carried on with Flatiron's bootcamp.

**Thoughts:** Started on JavaScript in the bootcamp prep, realised I'd forgotten a lot of it. 

**Learning Opportunities:**

**Link(s) to work** 

### Day 55: November 26

**Today:** Same as yesterday, SP and bootcamp prep.

**Thoughts:** Almost at the end of the 'Learn to Code' classes on SP! Which is rather exciting. There's a bunch of other learning classes, but they seem to be more rooted in 'life' leading to apps I'd actually use, like making a camera app.

**Learning Opportunities:**

**Link(s) to work** 

### Day 56: November 27

**Today:** Watched CS50 lecture 3, and did some classes on bootcamp prep.

**Thoughts:** lowercase to uppercase 

**Learning Opportunities:**

**Link(s) to work** 

### Day 57: November 28

**Today:** Started on a website for my brother's art piece, worked on bootcamp prep.

**Thoughts:**  Finding the right plugins is hard on WP... making things happen when you don't know any useful frameworks/languages on static sites is even harder. Bit of a hard day confidence wise, but trying to get back into my growth mindset, it just means I'm on ym way to learning more! 

But I think this had the biggest hit on my confidence: I had a run in with the unhelpful and patronising side of Stack Overflow. I asked a question about what I should do/where I should start with setting up the contact form on a static site, and recieved a downvote and very patronising answer with **bold** and *italic*, saying my question was too broad (even after I edited it). It reminded me that I'm entering into a world of lower emotional understanding than I'm used to (to be honest, most situations are like that when you've been studying psychology...). But just need to take a step back and remind myself that not everyone's going to be welcoming of newbies, and I need to make sure I'm clear about what I need (definitely a good life skill to have). Thankfully some helpful user arrived to my rescue and explained *why* and *how* my question was too broad and not appropriate for SO. The whole thing just reminded me how new I am to all this, and also to be careful of where (and how) I ask for help... 

**Learning Opportunities:**
At first I decided to use WordPress with Underscores for my brother's site, as although it's just a landing page, he was thinking about adding questionnaires etc, and although I could definitely learn how to do that on a static site, he needs it quite quickly and I'm definitely a lot more comfortable with WP at this point. However, after searching through plugins for about 2 hours I found **nothing** that was useful for what I needed. Which just happened to be an incredibly simple contact form including a drop down option for available dates. But apparently that's not simple (unless you want to spend money, which my brother does not want to do at this point). So then I started looking at a static site option and made some headway (as in I think I found what I was looking for). But then I realised I have no idea how to store the available dates and 'delete' them once someone's selected. I could learn, and it's definitely possible. But I have no idea where to start, and don't have the time for this project. Managed to at least get a contact form which sends emails onto the static site, thanks to [Reusable Forms](http://reusableforms.com/d/a/contact-form-bootstrap)! Have decided to sleep on it and either try the plugin route, or hope I can come up with the right question to ask on SO.

**Link(s) to work** 

### Day 58: November 29

**Today:** 

**Thoughts:** 

**Learning Opportunities:**

**Link(s) to work** 

### Day 59: November 30

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 60: December 1

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 61: December 2

**Today:** Watched the CS50 short video on fuctions (in C) and worked on the Flatiron bootcamp prep Javascript functions lessons.  

**Thoughts:** Too many functions today. I'd already been introduced to JS functions in my Skillcrush course, and then again in Swift in Playgrounds. So I have a good understanding of them. But wow, learning about them in C and getting deeper in JS within an hour of each other hurt my brain. I'm still getting used to the syntax of each language, so my brain had to work extra hard to not get them confused. It's definitely a lesson in making sure I compartmentalise my languages and review each one's syntax to not get them confused. Especially since I'm going to be adding Ruby into the mix in the next couple of days (and Python once I get further with CS50). In a way it's useful to learn multiple languages on the go, because I don't get caught up in the *language*, I learn how to *learn* and get comfortable with programming fundamentals (definitely a future blog post in there). It's also good training for my brain to work with more langauges at once, which I'll defintiely need to do in a job, but better to learn how to do it properly earlier on (before I get stuck in my ways). Anyway, ramblings. Hopefully each lanaguge will hepl me with the other in the courses. Though think I may do another quick JS course after this before I start any bootcamp so I am fully confident with it. 

**Learning Opportunities:** 

**Link(s) to work** 

### Day 62: December 3

**Today:** Javascript fundamentals for bootcamp prep. 

**Thoughts:**

**Learning Opportunities:** 
Was struggling with the Fix the Scope lab. Finally worked it out, but wanted to markup my reasoning to make sense of it.

`
\\defining funciton
var funkyFunction = function() { //assigns the the function 'function()' to variable funkyFunction 
  return function() {   //when function() is called, it will return itself, as the function is 'hidden' from the global variable
    return "FUNKY!"  //the function() function returns "Funky"
  }
}

// We want to set theFunk equal to "FUNKY!" using our funkyFunction.
// NOTE: you only need to modify the code below this line.
var theFunk = funkyFunction()   //assigns the funkyFunction() from above to the variable theFunk. This gets to the first level fo the original function up above, so it just returns the stringified version of function(), but doesn't get to "Funky"
theFunk = theFunk()   // assign theFunk variable as a function and call it, which gets into the next level
`

Not sure if that's right... going to come back to it once I've done some more reading.


**Link(s) to work** 

### Day 63: December 4

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 64: December 5

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 65: December 6

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 66: December 7

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 67: December 8

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 68: December 9

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 69: December 10

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 70: December 11

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 71: December 12

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 72: December 13

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 73: December 14

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 74: December 15

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 

### Day 75: December 16

**Today:**

**Thoughts:**

**Learning Opportunities:**

**Link(s) to work** 
