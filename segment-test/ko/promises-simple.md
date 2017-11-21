
비동기는 쉽지 않다고 생각합니다. 착수하려고 노력하고 있다면 동기 코드인 듯한 코드를 작성해 보세요. 이 경우에는 다음과 같이 합니다.

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

[체험해 보기](https://googlesamples.github.io/web-fundamentals/fundamentals/getting-started/primers/sync-example.html){: target="_blank" .external }


위 코드는 잘 작동합니다([코드](https://github.com/googlesamples/web-fundamentals/blob/gh-pages/fundamentals/getting-started/primers/sync-example.html){: target="_blank" .external } 참조)!
그러나 이는 동기 코드이고 다운로드하는 동안 브라우저를 잠급니다. 이를 비동기로 작동하게
하려면 `then()`을 사용하여 순서대로 발생하게 합니다.

