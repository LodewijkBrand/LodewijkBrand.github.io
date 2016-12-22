---
layout: post
title:  "Reinforcement Learning and Tetris"
date:   2016-12-3 22:04:31 -0800
categories: jekyll update
---

A great way to test the effectiveness of artificial intellegence algorithms is to use them to play games. We have seen the tangible results of various AI algorithms applied to video games like Space Invaders(Some algorithm), Mario (A*), etc. with great success:

Embed Space Invaders Video -- Embed Mario Video

Many of these algorithms rely on hand-crafted heuristics to direct the agent playing the game. This creates an interesting dilemma from a software engineering perspective because the engineer writing the software must know which stategies are "good" and which are "bad."

In order to overcome this knowledge dilemma we need to devise an algorithm that can play a game without prior knowledge. The agent is only provided with two pieces of information:
 - The agent is told when it "loses" or stops playing the game
 - The agent is rewarded when it "wins" the game.

A classmate of mine and I applied an algorithm developed by (AUTHOR) that took this approach in Backgammon and applied it to Tetris. The algorithm (known as TD-Gammon) is a reinforcment learning algorithm that relies on a neural network to approximate the score of a board configurations. Here's a rough idea of how that works in Tetris:

{% highlight java %}
// The Policy is where the magic happens! This is a neural network that
// tries to predict the the future score of a making a perticular move. 
// This policy is based entirely off of experience! So cool!
Policy tetris_policy;

for (int i = 0; i < NUM_GAMES; i++){
    Tetris current_game;

    while(current_game.playing()){
        // Explore to develop strategy!
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

Although I left some pieces out this elegant algorithm will (slowly) learn to play Tetris on it's own. A few things to keep in mind during the implementation:
 - How you encode the `current_game` state is up to you but it will have a significant impact on the performance of the algorithm.
 - Each pixel in the Tetris board was represented as a single neuron in a simple single-hidden-layer neural network in my implementation. It would be interesting to see the results using a convolutional neural network.
 - Remember that `exploit` should only happen after the algorithm has `explored` sufficiently.

If you're interested in a techincal analysis of the TD-Gammon algorithm as it applies to Tetris look [here]({{ site.url }}/assets/temporal_difference_in_tetris.pdf). The code behind the analysis can be found [here].
