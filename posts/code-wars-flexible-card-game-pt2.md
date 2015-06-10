---
title: 'Codewars: Flexible Card Game - 6 KYU Part 2'
date: '2015-05-31'
description:
tags: [ruby, codewars, kata]
---

In the second part of this post, I go over how I created the “Deck” class that passed the kata.
To see how created the “Card” class, check out my previous post “here.”

I create the Desk class that contains a constant variable called suits which contains an 
array of strings that each represent a type of suit. The class also has an accessor method
called cards which is initialized in the initialize method and ends up being an array containing
card objects representing each cards in a deck.

<pre class="prettyprint linenums">
  def initialize
    @cards = []
    SUITS.each do |suit|
      (1..13).each do |rank|
        card = Card.new(suit, rank)
        @cards &lt;&lt; card
      end
    end
  end
</pre>

I kind of cheat with the shuffle method and use the ruby shuffle method. At first the kata tests were not 
passing, but then I realized that the shuffle method was returning the cards array without it being shuffled.
So I added a bang “!” to the method, which actually “shuffles” the @cards array.

<pre class="prettyprint linenums">
  def shuffle
    cards.shuffle!
  end
</pre>

The count method is another easy method as it just returns the number of cards left in the deck.

<pre class="prettyprint linenums">
  def count
    cards.count
  end
</pre>

The drawn method takes a number as an argument (number 1 by default) and uses a range to remove
card objects from the deck. The cards array uses the pop() method to remove card objects and then adds
these cards to a drawn\_cards array. The drawn method then returns the drawn\_cards array in reversed\_order.

<pre class="prettyprint linenums">
  def draw(n = 1)
    drawn_cards = []
    (1..n).each do |x|
      removed_card = cards.pop()
      drawn_cards << removed_card
    end
    return drawn_cards.reverse()
  end
</pre>

And thats it! This solution passes all of the kata’s tests. If you have anything to add such as questions
or comments, please feel free to send them my way! The full code is found [here](https://github.com/djShrek/codewars/blob/master/Lvl%206%20Kyu/flexible_card_game.rb).
