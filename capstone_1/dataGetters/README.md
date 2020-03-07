## These notebooks contain routines for querying the API's of BreweryDB and Untappd.  

Since you can't just ask Untappd for a huge list of IPA ratings, or even a list of IPA's, you need to start by asking BreweryDB for a list of styles and then a list of all their beer listings for whichever styles you choose. That's covered in <b>BreweryDB IPA getter.ipynb</b>  

The resulting list of IPA's can then be used to query Untappd for checkins/ratings, but if you query by beer name, your results will pile up very slowly.  If you instead query by the brewers of those beers, you'll get at least as many ratings for those target beer names, plus a lot of other beers made by the queried brewery names.  That part is covered in <b>Joining Untappd and BreweryDB.ipynb</b>  

Now that you have a bunch of ratings, with an intentional bias towards IPA raters, you can speed up the process of amassing IPA checkins by querying the User Feed endpoint of the API for each of the users who showed up the most in the previous notebook.  This is done in <b>UserFeedGetter.ipynb</b>   

The above procedure seems to be the fastest way to accumulate the desired data, namely IPA checkins, but there are 2 features that are usually missing from the User Feed API endpoint, and I needed those 2 features in my analysis:  First, the Overall/Global Rating for each beer, and second, the text description of the beer as provided by the brewer.  The endpoints that contain those features are User Beer and Beer Info, which are queried in <b>UserBeerGetter.ipynb</b> and <b>Global Beer Adder.ipynb</b> to fill in the blanks.


