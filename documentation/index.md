---
layout: page
title:  "Documentation"
---

## Documentation

This is a very rough outline of the current workflow for collecting authors from publisher websites and conference programs, and how we are analyzing this data.

This is a very low-tec way of text mining and analysis, processes that have been formed out of convenience. This is not a definitive method for doing this work by any means.

To follow, you'll need a basic understanding of the Command Line, Excel, and the ability to understand what a PHP script is doing (not the ability to write PHP). 


# Collecting Book Authors
1. Find a way to download a data set from the publisher website
- We've had to be creative to collect and parse author names from publisher websites. Rather than copy/pasting each author name (which you're totally welcome to do), consider creating your own archive of the publisher website's title and author data for your particular topic. To do this, do the following:
	- Navigate to the publisher website
	- Find either the search/browse function and search for or browse books in your field from the past 5 years. 
		- This doesn't work the same way on all websites. If you're able to limit your search to 5 years, that's great. If not, you'll have to remember which year from the data will be your limit.
	- When your search returns, note if all the books in your query are in one list, or if there are multiple pages.
		- If all results are on one page, right click on the page, and click "Save As." Where it asks for file format, select "HTML" from the dropdown. Save to a directory where you'll be keeping author data.
		- If books are on multiple pages, I suggest creating one master HTML document rather than a bunch of documents. Right click on the page of results and click "View Page Source." A bunch of code will pop up in a new window. Copy and paste all of that code into a basic text editor, such as Notepad or Text Edit, and at a last resort, Microsoft Word. Repeat this step for each page of results and compile them into one document. Save that document as an HTML file in a dreictory where you'll be keeping author data.
	- Now you have a bunch of HTML! What are you going to do with that? 
		- What we need to do is use a script to PARSE all that information to extract all the authors.
		- In order to do that, we need to look at how the information is stored on the website to see how we should extract authors. 
		- Let's look at this example: 

				<div class="book-info">
					<a href="https://www.dukeupress.edu/soundscapes-of-liberation">
						<h3>Soundscapes of Liberation</h3>
						<h4>African American Music in Postwar France</h4>
					</a>
				<div class="b-meta-data">
					<a href="https://www.dukeupress.edu/soundscapes-of-liberation">By</a>
					<a class="author" href="https://www.dukeupress.edu/explore-subjects/browse?AuID=3908847">Celeste Day  Moore</a>
				</div>

		- In this example from Duke University Press, the author is always given as a link (the HTML tag 'a'), and the "class" of link is "author." That means that if we want to collect all the authors in the HTML code, we can write a code that looks for every < a class = "author" > and extracts just the author's name! 

2. Put that data set through a code that extracts just the author names and cleans it up
- I'm not a data scientist. But you can use your scholarly research skills to find some easy-to-run code if you know how to Google efficiently. To save time, I'll introduce the basic code I used to extract authors, and how you can run it as well. I'll also demonstrate how I rewrote the code for different types of author data storage in publisher website HMTL code.
	- Because I have some familiarity with the coding language "PHP," I decided to use PHP for this solution. But there are definitely other languages (Python, for example) that might be more efficient.
	- Your computer probably has PHP enabled. To run a PHP script, all you do is open your Command Line (Terminal on Mac or CommandPrompt (or whatever shell you use on Windows--see here for examples [add link]))
		- Then, you navigate to where your php script lives by changing the directory (type 'cd' into the prompt followed by where the php file lives).
			- Then, you simply type "php filename.php," and it runs!
		- But I've gotten ahead of myself. Just wanted to show you that you're totally capable of doing what I'm about to show you.
	- This is the basic PHP script that I, cobbled together from many free unlicensed sources on the internet and the experts at Stackverflow, came up with to parse HTML codes full of authors and extract their names:

			<?php

				$html = <<<HTML
					[INSERT HTML CODE HERE]
				HTML;

				$doc = new DOMDocument();
				$doc->loadHTML($html);
				foreach($doc->getElementsByTagName('a') as $a) {
    				if ($a->getAttribute('class') === 'author) {
        			$parts = explode('?', $a->getAttribute('href'), 2);
        			parse_str($parts[0], $output);

        			echo '' . $a->nodeValue . ", \n ";


    				}
				}
			?>

	- This code is saying, "this is PHP!" and then, "we're about to look at an HTML code!", and then look at "getelementsbytagname"--this is saying the HTML tag the script is looking for is 'a.' Then look ahead to 'getAttribute('class')--the class is "author." The rest of the code explains how to extract the name, and what format the name should be in the output. The part starting with "echo" tells the output to put a comma at the end of the name, which will come in handy later.
	- So, basically, you put that code into a blank file in Text Editor or Notepad, something basic, or Word if you don't have that, and you save it as a PHP extension with some type of name, I use "test.php". I also put this little note to myself (notes that shouldn't be read in the actual code you can put between < ! -- and -- > (without spaces!))

			< ! -- Use this script after downloading html(s) of book results. 
			Compile author/book details ONLY no other html into one html file and run script on the code.
			This script only parses authors if defined by a link class. Will need to copy and export to
			Excel and dedupe. Used on Duke University Press -- >

	- When you have HTML that you want to run through the code, copy and paste the entire code (yes it's a lot but I promise your computer can do it and it's easier than you finding all the parts you want) into the INSERT HTML CODE HERE section. Save the file (but be sure to erase the HTML after you're done with the next steps so that you have a clean slate for the next batch of author names)
	- Then go to your Command Line, locate the file you just created (cd) and then type "php filename.php"
		- If the script was unsuccessful, you'll see a bunch of warnings and you won't see any authors at all. 
		- If the script was successful, you'll probably still see warnings, because the script is also trying to parse parts of the code that have nothing to do with our script, and also becuase there may be other non-HTML elements in the code.
			- That's fine, ignore that and scroll til you see a list of names.
			- Those are all the author names! Find the first or last name, scroll down/up and select all those names. Copy and paste those author names into Excel, Google Sheets, Numbers, etc, just into a blank file for now. You can format that list of names later, just don't lose them.

	- There are so many different versions of this script that you can run for data that is formatted differently.
		- For example, this script parses any book data if defined by pargraph tags. Will need to copy and export to Excel and filter to just see authors and delete extra data and dedupe. (Used on OUP.)
				
				<?php

					$html = <<<HTML


					HTML;

					$doc = new DOMDocument();
					$doc->loadHTML($html);
					foreach($doc->getElementsByTagName('p') as $a) {
					$parts = explode('?', $a->getAttribute('p'), 2);

        			echo $a->nodeValue . "\n ";
					}
					?>

		- For example, this script only parses authors if defined by a DIV or LI class. Will need to copy and export to Excel and dedupe. (Used on U Michigan Press)

				<?php

					$html = <<<HTML


					HTML;

								$doc = new DOMDocument();
								$doc->loadHTML($html);
								foreach($doc->getElementsByTagName('span') as $a) 
								{ if ($a->getAttribute('class') === '[author') 
								{ $parts = explode('?', $a->getAttribute('span'), 0); 
								parse_str($parts[0], $output);
								echo '' . $a->nodeValue . ", \n ";
    					}
						}
						?>

		- And you can rewrite the script to work for any kind of author tag or formatting.

# Collecting Presenters
1. Unfortunately, collecting presenters is not as easy as downloading a data set usually. Typically, you will need to manually go through conference programs as PDFs.
- We are exploring easier ways of exporting with data collecting/scraping from Sched.

2. As you go through programs, collect first/last names and institutional affiliation (at the time) in an Excel spreadsheet

# Analyzing Affiliation
- Once you have the data for names, let's put it into Excel/Google Sheets
	- For Presenters, just enter this information in manually as you scan through the programs. 

1. First, make a table that has columns for all of the pertinent information that you need.
	- Necessary columns include:
		- Name
			- Names have been generated from the php script! Just copy and past them here.
		- Tenure Track
			- I think it's handy just to make this column a y/n.
			- I generate this information from a quick Google search, which I'll explain more below.
		- North America
			- Again, simple y/n column.
			- I generate this information from a quick Google search, which I'll explain more below.
		- Job
			- If not a tenure track professor, I use this column to write their job or status, like "independent scholar," "journalist," however the scholar chooses to present themselves.
				- Usually this comes from author bios, but sometimes I generate this information from a quick Google search, which I'll explain more below.
				- You can be descriptive in this column, generally it helps you do the qualitative part of this analysis, it's not factored into the quantitative equations in the sheet.
				- This can also be a good column to note if a non-tenure track scholar holds a PhD
		- Link
			- For "Link," I write an equation that makes a Google search link for each name so that it cuts down on the time you actually have to type into Google and search people.
				- On Excel, this formula is: =HYPERLINK(CONCATENATE("https:// www. google .com/search?q=",[CELL WITH NAME],"")) [without spaces]
	- Suggested columns:
		- Notes	
			- General notes for yourself, can be anything. 

2. After some light Googling, you can make the determination of what job they have, whether or not they are tenured, etc.
- Remember to keep any important data, like if they are in an associated scholarly field, left academia, etc., anything that may be pertinent for later data collection. You can use a broad "notes" column or more specific columns, whatever makes more sense to your data and subject.

3. Record that data to the best of your ability
- Also important to record if the scholar in question has a PhD for another layer of granularity. 

4. Calculations
- From the above information, you now how the power to find the following data points:
	- Total number of authors/presenters
	- Total number of authors/presenters from North America
	- Total tenure track professors
	- Tenure track professors from North America
	- Non-tenure track from North America
		- Non-tenure track but university affiliated
	- Non-tenure track Total
	- Number of totally independent scholars
		- This is the number of North American non-tenure track scholars who are not affiliated with a university.
	- Number of PhD holders from North America, non-tenure track, non-affiliated
	- Number of totally independent scholars without a PhD

	From this data, you can calculate:
	- Percentage of totally independent authors/presenters from North America
	- Percentage of non-tenure track, non-traditionally affiliated authors/presenters from North America
	- Percentage of PhD authors/presenters from North America who are unaffiliated
