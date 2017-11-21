Let's put it all together:

    getJSON('story.json').then(function(story) {
      addHtmlToPage(story.heading);

      return story.chapterUrls.reduce(function(sequence, chapterUrl) {
        // Once the last chapter's promise is done…
        return sequence.then(function() {
          // …fetch the next chapter
          return getJSON(chapterUrl);
        }).then(function(chapter) {
          // and add it to the page
          addHtmlToPage(chapter.html);
        });
      }, Promise.resolve());
    }).then(function() {
      // And we're all done!
      addTextToPage("All done");
    }).catch(function(err) {
      // Catch any error that happened along the way
      addTextToPage("Argh, broken: " + err.message);
    }).then(function() {
      // Always hide the spinner
      document.querySelector('.spinner').style.display = 'none';
    })

[Try it](https://googlesamples.github.io/web-fundamentals/fundamentals/primers/async-example.html)

And there we have it (see
[code](https://github.com/googlesamples/web-fundamentals/blob/gh-pages/fundamentals/primers/async-example.html)),
a fully async version of the sync version. But we can do better. At the moment
our page is downloading like this:
