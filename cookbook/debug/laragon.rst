.. _rst_cookbook_debug_laragon:

Laragon
===============

Cmder
SSH
dans le fichier `bin\cmder\config\user-profile.cmd`, la ligne

`call "%GIT_INSTALL_ROOT%/cmd/start-ssh-agent.cmd"` retirer les « :: » pour la décommenter...

si cela ne fonctionne pas, en console

ssh-agent -s
ssh-add ~/.ssh/mm_ssh (saisir le mot de passe si besoin)

.. |img_symfony-toolbar| image:: /_img/screenshots/cookbook/debug/symfony-toolbar.jpg
