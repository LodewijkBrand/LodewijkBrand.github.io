---
layout: post
title:  "Reinforcement Learning and Tetris"
date:   2016-12-3 22:04:31 -0800
categories: jekyll update
---

A great way to test the performance of various artificial intelligence algorithms is to use them to play games! We have seen the tangible results of various AI algorithms applied to video games like Space Invaders, Mario, and others, with great success:

<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/DlkMs4ZHHr8" frameborder="0" allowfullscreen></iframe></p>

Many of these algorithms rely on hand-crafted heuristics to direct the agent playing the game. This creates an interesting dilemma from a software engineering perspective because the engineer writing the software must know which strategies are "good" and which are "bad."

In order to overcome this knowledge dilemma we need to devise an algorithm that can play a game without prior knowledge. The agent is only provided with two pieces of information:
 - The agent is told when it "loses" or stops playing the game
 - The agent is rewarded when it "wins" the game.

Here's another Mario AI agent that has learned to play without the help of hand-crafted heuristics. The strategy is extremely different:

<p align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/EZLkCdMXw8g" frameborder="0" allowfullscreen></iframe></p>

A classmate of mine and I applied a similar algorithm developed by Gerald Tesauro to play Tetris. Tesauro used this algorithm to have an agent learn to play backgammon on its own. The approach (known as TD-Gammon) is a reinforcement learning algorithm that relies on a neural network to approximate the future "score" of board configurations. Here's a rough idea of how that works in Tetris:

{% highlight java %}
// The Policy is where the magic happens! This is a neural network that
// tries to predict the the future score of a making a particular move.
// This policy is based entirely off of experience! So cool!
Policy tetris_policy;

for (int i = 0; i < NUM_GAMES; i++){
    Tetris current_game;

    while(current_game.playing()){
        // Explore to develop new strategies
        Move move = current_game.getRandomMove();

        if (exploit){
            //Use my policy to make the best move
            current_score = tetris_policy.score(current_game, move);
	    for (Move tmp_move : current_game.getValidMoves()){
                tmp_score = tetris_policy.score(current_game, tmp_move);
                if (tmp_score > current_score){
                    move = tmp_move;
                    currentScore = tmp_score;
                }
	    }
	}

	current_game.makeMove(move); // Make our move! (Exploit or Explore)
	tetris_policy.update(current_game); // Update policy based on outcome
    }
}
{% endhighlight %}

Through testing we found that this algorithm will (slowly) learn to play Tetris on it's own. Here are a few things to keep in mind during the implementation:
 - How you encode the `current_game` state is up to you but it will have a significant impact on the performance of the algorithm.
 - Each pixel in the Tetris board was represented as a single neuron in a simple single-hidden-layer neural network in my implementation. It would be interesting to see the results using a convolutional neural network.
 - Remember that `exploit` should only happen after the algorithm has `explored` sufficiently.

If you're interested in a technical analysis of the TD-Gammon algorithm as it applies to Tetris look [here]({{ site.url }}/assets/temporal_difference_in_tetris.pdf).

The code behind the analysis can be found [here](https://github.com/LodewijkBrand/Tetris).
