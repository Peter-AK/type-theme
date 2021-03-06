---
layout: post
title: You sunk my BattleShip! [GUI with PyQt5]

---
<table>
  	<tr>
    	<th style="text-align: center; vertical-align: middle;">
    		<img src="{{ site.baseurl }}/assets/img/posts/post2/battleship_icon.png" height="110" width="170" style="border:5px solid black" align="middle">
    	</th>
    	<th>
    		<a href="https://github.com/Peter-AK/Battleship"><img src="https://gh-card.dev/repos/Peter-AK/Battleship.svg"></a>
    	</th>
  	</tr>
  	<tr>
    	<td colspan="2">
    		My take on a classic pencil and paper game with Python. The main challenges here are:
			&nbsp;<li> 1) To create a competitive AI that can make good logical choices.
			<br> &emsp;&emsp; Possible look into implementation of pre-made algorithms.</li>
			&nbsp;<li> 2) Integrate everything with a smooth GUI/User experience using Qt for python.
			<br> &emsp;&emsp; I don't have much experience with GUI architecture, probably will be the most challenging part to do right.</li>
		</td>
  	</tr>
</table>

<table>
	<tr>
    	<td  style="background-color:#eaeaea">
			<h2> The Rules: </h2>
			<b><br>Thursday, June 18, 2020
			<br>===============================</b>
			<p style="text-align:left;">Over the years there have been couple of variations of the game BattleShip from what the wikipedia page tells me.
			<br>The <a href="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e4/Battleships_Paper_Game.svg/2000px-Battleships_Paper_Game.svg.png"> Samuel Bednar</a> version seems to be quite an interesting choice and the one that I will be model the game after.</p>
			<p>Setup the following ships on your 10x10 grid:
			<h3>Fleet of Ships</h3>
			<table>
				<tr>	
				<th>Ship</th>	<th>Size</th>	<th>Quantity</th>
				</tr>
				<tr>
				<td>Carrier</td>	<td>5</td>	<td>1</td>
				</tr>
				<tr>
				<td>Battleship</td>	<td>4</td>	<td>1</td>
				</tr>
				<tr>
				<td>Cruiser</td>	<td>3</td>	<td>1</td>
				</tr>
				<tr>
				<td>Destroyer</td>	<td>2</td>	<td>2</td>
				</tr>
				<tr>
				<td>Submarine</td>	<td>1</td>	<td>2</td>
				</tr>
				</table></p>
			<p>Each round the player will fire a number of salvos corresponding to the number of ships that are alive.
			<br>The selection of grid spaces to attack will happen during the turn, the shots will be fired simultaneously at the end of the turn. The player will find out if he had hit something at the end of his turn.</p>
			<p>(Since a player has multiple shots during a given turn [unless he has 1 ship left], I think it's for the best that he only finds out at the end of the turn whether they hit. Otherwise it will give a big disadvantage to the player who starts second.)</p>
			<p>The player who kill all his enemy's ships will win </p>
		</td>
		<td  style="background-color:#eaeaea">
			<div align="middle"><img src="https://upload.wikimedia.org/wikipedia/commons/e/e4/Battleships_Paper_Game.svg"  style="border:2px solid black ">
			</div><div align="right"> Figure 1. : A typical pen-and-paper version of the game.</div>
		</td>
  	</tr>
  	<tr>
    	<td  style="background-color:#d0d0a5">
			<h2> The Back-end: </h2>
			<b><br>Saturday, June 06, 2020 (updated: June, 18)
			<br>===============================</b>
			<p style="text-align:left;">I want this project to have a fully functional back-end before I start my work on the GUI. The idea is to have a class called Player,
			<br>this class will have a grid setup function that will be ran during its __init__ method.</p>
			<p style="text-align:left;">A PC subclass will inherit Player, with an addition of random module, and therefor the pc can setup run its own own ships setup by using random inputs.
			<br>(I don't think its necessary to add logic to ship placement since randomizing their locations seems like a fine strategy for me.)</p>
			<p>Ship will be another class shared by both player/pc, they will have all the info allocated to each ship (its position etc..), and will be used to update ships status on the grid.</p>
		</td>
		<td  style="background-color:#d0d0a5">
		<br>
		<br>
			<div align="middle"><img src="{{ site.baseurl }}/assets/img/posts/post2/jun-06.png"  style="border:2px solid black "><div align="right"> Figure 2. : Ship testing placement.</div>
			</div>
		</td>
  	</tr>
	  <tr>
    	<td  style="background-color:#eaeaea" colspan='2'>
			<b><br>Saturday, June 21, 2020
			<br>===============================</b>
			<p> The structure for the back-end in mostly completed. Only minimum AI has been implemented so far, the opponent <br>will not shoot at previous location he shot in before. Other then that all the PC selection is random so far.</p>
			<p> The work towards building a GUI for the game has started.</p>
			<div align="middle"><img src="{{ site.baseurl }}/assets/img/posts/post2/workflow.png" height="450" width="750" style="border:2px solid black ">
			</div><div align="right"> Figure 3. : Back end object interaction overview.</div>
		</td>
  	</tr>
	<tr>
    	<td style="background-color:#d0d0a5">
			<b><br>Saturday, July 07, 2020 (updated: Aug, 03)
			<br>===============================</b>
			<p> &nbsp;The GUI development so far has been a bit slow due to other work getting in the way and the fact that I'm pretty new the the Qt framework. </p>
			<p>The setup interface is almost done. The interface uses the same back-end logic,<br> a) takes one anchor point <br>b) generates all possible end location based on the ships length.<br> The only adjustment made to the back-end was how it receives the user inputs. </p>
			<p> The button grid is generated via a for loop and placed in a QButtonGroup with an ID based on it's location. I use this button id to do most of the manipulations.</p>
		</td>
		<td style="background-color:#d0d0a5">
		<br>
		<br>
			<div align="middle"><img src="{{ site.baseurl }}/assets/img/posts/post2/setup_gui.gif"  style="border:2px solid black "><div align="right"> Figure 4. : Setup GUI screen.</div>
			</div>
		</td>
  	</tr>
	  <tr>
    	<td  style="background-color:#eaeaea" colspan='2'>
			<b><br>Saturday, June 21, 2020
			<br>===============================</b>
			<p> The structure for the back-end in mostly completed. Only minimum AI has been implemented so far, the opponent <br>will not shoot at previous location he shot in before. Other then that all the PC selection is random so far.</p>
			<p> The work towards building a GUI for the game has started.</p>
			<div align="middle"><img src="{{ site.baseurl }}/assets/img/posts/post2/combat_gui.gif" height="350" width="750" style="border:2px solid black ">
			</div><div align="right"> Figure 5. : Back end object interaction overview.</div>
		</td>
  	</tr>
	<tr>
    	<td style="background-color:#d0d0a5" colspan='2'>
			<b><br>Friday, December 11, 2020 
			<br>===============================</b>
			<p> &nbsp; Configuration for GUI interface with PyQt5</p>
			<div align="left"><img src="{{ site.baseurl }}/assets/img/posts/post2/splash_screen.PNG" style="border:2px solid black " height="350"><div align="right"> Figure 6. : Splash screen GUI.</div>
			</div>
		</td>
  	</tr>
		<tr>
		<td style="background-color:#d0d0a5" colspan='2'>
			<div align="middle"><img src="{{ site.baseurl }}/assets/img/posts/post2/setup_gui.PNG" style="border:2px solid black "><div align="right"> Figure 7. : Setup GUI.</div>
			</div>
		</td>
  	</tr>
</table>

