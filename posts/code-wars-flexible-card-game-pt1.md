---
title: 'Codewars: Flexible Card Game - 6 KYU Part 1'
date: '2015-05-30'
description:
tags: [ruby, codewars, kata]
---

I really liked this simple kata because it tests one’s ability to properly create classes and 
knowledge of object-oriented programming.

Description of kata found [here](http://www.codewars.com/kata/5436fdf34e3d6cb156000350)

Essentially, you are creating a “Deck” class and a “Card” class that can be used and modified to create different types of card games.

The Deck class has 1 public attribute “cards” 3 public methods: count(), shuffle(), and  draw(n). 
The Card class has 2 public attributes including “suit” and “rank” with 2 public methods face_card? and a to_s method. The cards must also be comparable to other cards, so the Ruby Comparable module will be used to compare the ranks of the cards only.

I first start with the card class and begin by including the Comparable module. Now the card class will be able to use operators such has <=> (spaceship?) operator to compare other cards.

<pre class="prettyprint linenums">
class Card
  include Comparable ## 1
end
</pre>

Then I create a constant variable that will hold a hash which maps numbers to their respective face card values. 
Example: 11 => “jack”, 12 => “queen”, 13..etc etc.

<pre class="prettyprint linenums">
FACE_CARDS = { 11 => "jack", 12 => "queen", 13 => "king", 1 => "ace" }
</pre>

I create the 2 public attributes using attr_accessor methods for both :suit and :rank. I could have just gone with attr_reader but I think I was more focused on finishing the class. Bad habits I know :(

<pre class="prettyprint linenums">
  attr_accessor :suit
  attr_accessor :rank
</pre>

The initialize method simply sets up instance variables for @suit and @rank.

<pre class="prettyprint linenums">
  def initialize(suit, rank)
    @suit = suit
    @rank = rank
  end
</pre>

The face_card? method returns true if rank of the card is above 10, which suggests it will either be a Jack, Queen or King..Or else, return false.

<pre class="prettyprint linenums">
  def face_card?
    return true if rank > 10
    false
  end
</pre>

  The to_s method is a method that returns a string describing the card in a English sentence.
     My strategy was to check the FACE_CARDS constant against the cards rank and if it had the rank
     return the corresponding string with the name of the face card and suit,  or else just return 
     the rank and suit of the card.

<pre class="prettyprint linenums">
  def to_s
    if FACE_CARDS.has_key?(rank)
      return "#{FACE_CARDS[rank].capitalize} of #{suit.capitalize}"
    end
    "#{rank} of #{suit.capitalize}"
  end
</pre>

Finally, the last method is the spaceship? operator that compares the rank of card1 to another card.
     If the card is greater than the other card, return 0, if equal, return 0, or else return -1

<pre class="prettyprint linenums">
  def <=>(card2)
    if self.rank > card2.rank
      return 1
    elsif self.rank == card2.rank
      return 0
    else
      -1
    end
  end
</pre>

and thats it! 