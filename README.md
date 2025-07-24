Object-Oriented Sets
For this part, you will earn credit by completing the TweetSet.scala file. This file defines an abstract class TweetSet with two concrete subclasses, Empty which represents an empty set, and NonEmpty(elem: Tweet, left: TweetSet, right: TweetSet), which represents a non-empty set as a binary tree rooted at elem. The tweets are indexed by their text bodies: the bodies of all tweets on the left are lexicographically smaller than elem and all bodies of elements on the right are lexicographically greater.

Note also that these classes are immutable: the set-theoretic operations do not modify this but should return a new set.

Before tackling this assignment, we suggest you first study the already implemented methods contains and incl for inspiration.

1 Filtering
Implement filtering on tweet sets. Complete the stubs for the methods filter and filterAcc. filter takes as argument a function, the predicate, which takes a tweet and returns a boolean. filter then returns the subset of all the tweets in the original set for which the predicate is true. For example, the following call:

tweets.filter(tweet => tweet.retweets > 10)

applied to a set tweets of two tweets, say, where the first tweet was not retweeted and the second tweet was retweeted 20 times should return a set containing only the second tweet.

Hint: start by defining the helper method filterAcc which takes an accumulator set as a second argument. This accumulator contains the ongoing result of the filtering.

/** This method takes a predicate and returns a subset of all the elements
 *  in the original set for which the predicate is true.
 */
def filter(p: Tweet => Boolean): TweetSet
def filterAcc(p: Tweet => Boolean, acc: TweetSet): TweetSet

The definition of filter in terms of filterAcc should then be straightforward.

2 Taking Unions
Implement union on tweet sets. Complete the stub for the method union. The method union takes another set that, and computes a new set which is the union of this and that, i.e. a set that contains exactly the elements that are either in this or in that, or in both.

def union(that: TweetSet): TweetSet

Note that in this exercise it is your task to find out in which class(es) to define the union method (should it be abstract in class TweetSet?).

Warning : This method is a crucial part of the assignment. There are many ways to correctly code it, however some implementations run in an exponential time, so be careful, an inefficient implementation might result in a timeout during the grading process.

3 Sorting Tweets by Their Influence
The more often a tweet is "re-tweeted" (that is, repeated by a different user with or without additions), the more influential it is.

The goal of this part of the exercise is to add a method descendingByRetweet to TweetSet which should produce a linear sequence of tweets (as an instance of class TweetList), ordered by their number of retweets:

def descendingByRetweet: TweetList

This method reflects a common pattern when transforming data structures. While traversing one data structure (in this case, a TweetSet), we're building a second data structure (here, an instance of class TweetList). The idea is to start with the empty list Nil (containing no tweets), and to find the tweet with the most retweets in the input TweetSet. This tweet is removed from the TweetSet (that is, we obtain a new TweetSet that has all the tweets of the original set except for the tweet that was "removed"; this immutable set operation, remove, is already implemented for you), and added to the result list by creating a new Cons. After that, the process repeats itself, but now we are searching through a TweetSet with one less tweet.

Hint: start by implementing the method mostRetweeted which returns the most popular tweet of a TweetSet
