The competitor site is loading slow at the very start where we first see a blank page for some time. Our page loads straight to the list very fast. Slower performance of competitor site is also do to more complex design and content.

Competitor site have more features then our app like saving different lists, adding to-do's for specific dates, sorting of the list, categories, drag and drop and printing option.

The speed index of competitor site is not so good because visible content needs some time to populate the page.

One of the things for future upgrades on which one we need to pay attention is the leverage of the font-display CSS feature to ensure text is user-visible while web fonts are loading. That is one way to avoid a blank page at the beginning of loading and to speed the page to load up.

The second thing to improve can be reducing JavaScript execution time. That means a revision of the code and make him execute only when needed. That is especially important on the first load when it is not needed for all code to be executed if it is not needed to do anything at the moment.

Since this page uses HTTP/1.1 protocol that will lead to slower loading time. The suggestion is that for all future upgrades we always use the HTTP/2 protocol.

Image elements on this site do not have their explicit width and height and that can cause page loading to be messy with text going all over the place while with every image load page will reflow. By giving every image an explicit width and height, the browser will know the aspect ratio of the image which will allow the browser to calculate and reserve sufficient space for the height and associated area. That way user experience is much better.

Performance test detected 28 static resources that are not cached (or have very short cache time) but instead always loading on every visit to the page. A long cache lifetime can speed up repeat visits to the page. Because of it, Largest Contentful Paint is very slow.
