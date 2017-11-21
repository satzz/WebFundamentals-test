
Thinking async isn't easy. If you're struggling to get off the mark,
try writing the code as if it were synchronous. In this case:

    try {
      var story = getJSONSync('story.json');
      addHtmlToPage(story.heading);

      story.chapterUrls.forEach(function(chapterUrl) {
        var chapter = getJSONSync(chapterUrl);
        addHtmlToPage(chapter.html);
      });

      addTextToPage("All done");
    }
    catch (err) {
      addTextToPage("Argh, broken: " + err.message);
    }

    document.querySelector('.spinner').style.display = 'none'

[Try it](https://googlesamples.github.io/web-fundamentals/fundamentals/primers/sync-example.html)


That works (see
[code](https://github.com/googlesamples/web-fundamentals/blob/gh-pages/fundamentals/primers/sync-example.html))!
But it's sync and locks up the browser while things download. To make this
work async we use `then()` to make things happen one after another.
