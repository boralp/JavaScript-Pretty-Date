# JavaScript-Pretty-Date
John Resig's javascript date function on GitHub.

JavaScript Pretty Date

One method that I’ve been wanting for quite a while now was a simple way to format old JavaScript dates in a “pretty” way. For example “2008-01-28T20:24:17Z” becomes “2 hours ago”. Here’s some more examples:

prettyDate("2008-01-28T20:24:17Z") // => "2 hours ago"
prettyDate("2008-01-27T22:24:17Z") // => "Yesterday"
prettyDate("2008-01-26T22:24:17Z") // => "2 days ago"
prettyDate("2008-01-14T22:24:17Z") // => "2 weeks ago"
prettyDate("2007-12-15T22:24:17Z") // => undefined
Note that I only care about dates in the past (by far the most common use case) and only dates within the past month (anything beyond a month becomes fuzzy and impractical).

JavaScript Pretty Date

pretty.js (Also include a .prettyDate() jQuery plugin, for convenience.)
Demo (Some examples of date conversion using basic DOM manipulation.)
Example Usage

In the following examples I make all the anchors on the site, that have a title with a date in it, have a pretty date as their inner text. Additionally, I continue to update the links every 5 seconds after the page has loaded.

With plain DOM:

function prettyLinks(){
    var links = document.getElementsByTagName("a");
    for ( var i = 0; i < links.length; i++ )
        if ( links[i].title ) {
            var date = prettyDate(links[i].title);
            if ( date )
                links[i].innerHTML = date;
        }
}
prettyLinks();
setInterval(prettyLinks, 5000);
With jQuery:

$("a").prettyDate();
setInterval(function(){ $("a").prettyDate(); }, 5000);
About

There’s a variety of these functions around, in various languages, but I wanted one in JavaScript for a couple reasons:

Microformats – Microformats specify a scheme for passing ISO dates to the client (precise date/time value) while providing the user with a “casual” date representation. I wanted to be able to generate a pretty version of the date, from a Microformat, easily and painlessly.

Auto-update – Secondly, I wanted to have these Microformat dates update automatically, as the page remained loaded. This way, if a user left a page open for 15 minutes, and came back, the pretty dates would be silently updated to their current times. This may seem nitpick-y but Twitter fails to do this and it drives me absolutely insane.

Write once, use everywhere – If I wanted to have these dates be constantly updated I would have these options: Only generate these dates on the server – re-querying new results via an Ajax request, generate the results on the server and on the client, or generate the results exclusively on the client. Client makes the most sense as it would result in the least amount of code duplication and general overhead.

I hope this will be useful to some, I know it’s helped me out a bunch.

By the way – let’s say this piece of code was from a – theoretical – larger project that was attempting to create an easy-to-use, Open Source, Twitter clone – would anyone be interested in using it?

Posted: January 29th, 2008
