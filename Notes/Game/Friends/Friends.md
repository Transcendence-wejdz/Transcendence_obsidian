---
graph-size: 200
---
#module #game

Liste d'amis et invitations à une session.

## Scripts

- <a href="#vault://../UnityProject/Assets/Scripts/Friends/FriendsManager.cs" class="LinkRelativeTo">FriendsManager.cs</a> — logique d'invitation (anti-spam ; inviter en hostant ferme d'abord ta propre session en cours)
- <a href="#vault://../UnityProject/Assets/Scripts/Friends/FriendsPanelUI.cs" class="LinkRelativeTo">FriendsPanelUI.cs</a> / <a href="#vault://../UnityProject/Assets/Scripts/Friends/FriendRowUI.cs" class="LinkRelativeTo">FriendRowUI.cs</a> — liste UI des amis
- <a href="#vault://../UnityProject/Assets/Scripts/Friends/InviteToastUI.cs" class="LinkRelativeTo">InviteToastUI.cs</a> — toast d'invitation entrante

## Connexions

- → [[Networking]] : une invitation pointe vers une session hostée via `NetworkBootstrap`
