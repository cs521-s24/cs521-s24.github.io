---
layout: assignment
due: 2024-05-07 23:59:59 -0800
permalink: assignments/project05.html
title: Project05 - HTTP Server
github_url: https://classroom.github.com/a/JHL0f7cS
published: false
---

{% assign img_base = site.url | append: site.baseurl | append: "/assets/img" %}

## Requirements

1. In this project, you will evolve the TCP socket (lab06) and a basic HTTP server (lab07) into a more capable HTTP server. 
1. You will add support for [path](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/What_is_a_URL#path_to_resource) and embedded compontents such as [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) files in HTML. Note that you do not need to write a client-side program that handles CSS or any other HTML formatting. Your web browser will take care of it. 

## Example output

1. You need to set up SSH port forwarding. If you were using port 9000 (use the same port number you used for lab06 and lab07) in a container, then open a second terminal and run the following command to get your container's IP address
	```sh
	$ clabip
	172.17.0.22
	```
1. Run a terminal on your laptop and run this command so that your web browser's connection to `localhost` on port 9000 will be forwarded to your container on port 9000.

	```sh
	$ ssh -J stargate -L 9000:172.17.0.22:9000 medusa
	```

1. Go to localhost:9000 on your web browser. Your HTTP server running in your container should respond. For the content of your server, use the content of CS521 website ![as shown below]({{ img_base }}/project05_screenshot.png).

1. Click on the links - the contents must match what you would see on the official CS521 website. 

## Implementation notes

1. Download the content of cs521 course website to serve from your own web server. To scrape the site, run

	```sh
	$ wget --recursive --page-requisites --convert-links cs521-s24.github.io
	```
1. If you wish to store the content in `www` directory, move the contents as follows.
	```sh
	$ mv cs251-s24.github.io www
	```
1. You may use `fseek()` and `ftell()` function to get the size of the file for the `Content-Length: ` part. The following line puts the file position indicator for the stream pointed to by `stream`to the end of the file, and `ftell(stream)` returns the current offset (position) in bytes. 

	```sh
	(void) fseek(stream, 0L, SEEK_END)
	```



	Once the stream reaches the end of the file, you can use `rewind()` or `fseek()`. The following commands set the file position indicator for the stream pointed to by `stream` to the beginning of the file, so that your program can read the file and send it over the socket.

	```sh
	(void) rewind(stream)
	```

	```sh
	(void) fseek(stream, 0L, SEEK_SET)
	```

1. You may use `strsep()` function to get the directory and file names from the URL. 


## Grading process

1. Project05 will be interactively graded by peers on Thu, May 9th, the last class day of the semester using the rubric below. 
	1. Everyone will submit a google form with the scores. TAs will review for an error in grading and enter the scores in Canvas.
	1. An absence during the peer-grading session will result in 0 for project05. 
	1. Note that there is no resubmission for Project05 style. The peer-grading session happens on the last class day, so there is no time for resubmission and regrading. 
    1. Grading meetings must use the clab terminal environment, not local IDEs on your laptop or web pages on github.com
    1. To ensure that everyone has the same deadline, grading meetings will start with `grade clone -p project05 -s your_github_id -d 2024-05-08` to get a clean repo

## Rubric

1. We will use the following rubric during peer-grading session.
	1. `path` support (40 pts): 
		1. The contents served from the HTTP server match what are served from the official CS521 website. 
	1. using non-blocking IO and `poll` (40 pts): 
		1. check the source code for the correct use of `ioctl`
		1. check the source code for the correct use of `poll` 
	1. Defensive coding (10 pts):
		1. Checking for memory and I/O errors (3 pts)
		1. No unbounded memory copies (3 pts)
		1. No memory leaks (4 pts)
	1. Style (10 pts): 
		1. Consistent naming and indentation (2 pts)
		1. Well-designed functions	(2 pts) 
		1. Helpful comments (2 pts)	
		1. No dead (commented-out) code or unnecessarily complex code (2 pts)	
		1. No build products or output dictionary files in the repo (2 pts)

