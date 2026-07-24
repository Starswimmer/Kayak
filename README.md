SentientSands Kayak, Living AI NPCs for Kenshi

CREDITS
SentientSands Kayak by Harvicus and Pineaxe
Original SentientSands concept and foundation: Harvicus
Kayak and most of the current release development: Pineaxe
Contributors: Wirlocke and ConcreteFoundry
Special thanks to BFrizzleFoShizzle and the RE_Kenshi and KenshiLib contributors.

SHORT DESCRIPTION
Talk to almost anyone in Kenshi through an LLM. Characters remember you, react to the world, speak to each other, spread rumors and act on conversations, powered by Kayak’s persistent lore and campaign knowledge system.

ABOUT SENTIENTSANDS KAYAK
SentientSands connects Kenshi’s characters and world systems to a Large Language Model.
This is more than a chatbot placed over the game. NPCs receive information about their identity, faction, race, location, health, equipment, relationships, memories and recent events. Their responses depend on who they are, what they know and what is happening around them.
Kayak expands the original mod with a persistent, campaign based knowledge system. It provides deeper access to Kenshi lore, factions, locations, species, items, NPC histories and custom world information, while giving players and modders much more control over what the AI knows and how it responds.

FEATURES
• Talk to almost anyone
Select an NPC and open the chat window. Conversations are generated in real time using the character’s identity, personality, backstory, faction, condition, surroundings and knowledge of the world.
• Talk, Whisper and Yell
Talk normally, whisper privately to one character, or yell to a group and receive responses from multiple nearby NPCs.
• Persistent identities and memories
Generic characters can receive unique names, personalities and backstories. Their profiles, dialogue histories and memories are stored inside your campaign, allowing them to recognize you and remember previous encounters.
• A living, talkative world
Nearby NPCs can speak to each other without player input. They may react to battles, injuries, hunger, local conditions, faction activity, your squad and other events happening around them.
• World history and rumors
Important events can become part of the campaign’s living history. News of battles, deaths, rescues, raids and conquered towns may spread through conversations and rumors.
• Dialogue with consequences
Depending on the NPC, your relationship and the selected AI model, conversations can lead to recruitment, trading, attacks, imprisonment, faction relation changes and other in game actions.
• Kayak Knowledge Engine
Kayak retrieves relevant information about factions, cities, regions, species, characters, items and lore instead of sending the AI a single giant block of generic information. Characters can know different things depending on who they are and where they belong.
• Multiple campaigns
Each campaign keeps its own characters, memories, dialogue history, world events, rumors and custom lore. Different playthroughs can remain completely separate.
• In game F8 Hub
Use the F8 menu to select AI providers and models, test your connection, configure dialogue settings, manage campaigns, browse previous conversations and inspect world rumors.
• Choose your own AI
Use Player2 for a simple setup, connect to services through an OpenAI compatible API, or run supported local models through applications such as Ollama or LM Studio.
• Player customization
Profiles, personalities, speech styles, backstories, prompt rules and world knowledge are stored in readable files. Advanced users can also use in game commands to edit characters, manage data, control actions and customize how the system behaves.
• SentientSongs
The optional SentientSongs system allows music stored on your computer to be played and controlled through in game commands, including songs, folders, playlists, volume, shuffle and loop controls.
• Language support
Included language support should cover English, Spanish, French, Japanese, Russian, Turkish and Chinese. This feature is old and it's not guaranteed to work, reffer to our discord for assistance on this topic.

QUICK FAQ
Q: What do I need to run the mod?
You need Kenshi, Python, the latest RE_Kenshi, and access to an AI model. The AI can come from Player2, an OpenAI compatible provider, or a supported local server.
Place SentientSands folder inside your kenshi mods folder, open SentientSands folder and click on INSTALL_DEPENDENCIES.bat this will setup the moditself, provided you have the latest python version installed on your computer. After that, you'll need to choose a provider and model, on the .JSON files that should open after the installation is complete. Activate the mod on your modlist as any other, open the game, load a save, press F8, go on settings, make sure your provider and model are selected and click on "Test". If it fails, the best way to find what's wrong is by joining our discord server provided at the end of this text.

Q: Is an AI subscription required?
No specific subscription is required. Some providers charge for usage, some offer free access or limited credits, and local models can run on your own computer. Response quality and hardware requirements vary considerably between models.

Q: How do I start after installing?
Launch Kenshi with the mod enabled, load your save and press F8. Open Settings, choose your provider and model, save the settings, reopen Settings and use the connection test. After receiving an “LLM Okay” response, create or select a campaign.

Q: Can I use an existing Kenshi save?
Yes. Create a SentientSands campaign for that playthrough. We recommend using a separate campaign for each save so that characters, memories and world events do not become mixed together.
Campaigns created before SentientSands Kayak v0.4 are not compatible with the current campaign format.

Q: Why are the conversations repetitive, strange or out of character?
The selected AI model makes a very large difference. Small or heavily restricted free models may produce weaker dialogue. Also confirm through the F8 connection test that your provider is working and that the Kayak server started correctly.
Character personalities, backstories and prompt rules can also be edited if you want a different style.

Q: Does the mod remember every conversation forever?
Dialogue history and character information are stored in campaign files. History limits can be configured, and individual character histories or profiles can be cleared when needed. In short, the memory of the NPC comes from two places: The last configurable quantity of dialogue lines, and the npc profile. The npc profile can be manually updated, which should add the general personality changes from those dialogue lines.

Q: Can NPCs really recruit, trade or attack through dialogue?
Yes, the mod includes action systems connected to conversations. Results depend on the character, faction relations, circumstances, prompt interpretation and the ability of the selected model to follow the action format correctly.
Direct commands are also available for players who prefer explicit control.
The ATTACK command, however, is aimed at your player character. Which means it won't order an npc to "enter attack mode against your enemies", instead, it will make that npc attack YOUR character. This can be used, for example, to create a training/sparring situation. After that you can use the mod's commands to stop the fight and make a character rejoin your squad or, if it's not a member of your squad, you can use a command to make him not-hostile again.

Q: Does the mod send information to an external service?
When using an online provider, dialogue and game context required to generate the response are sent to that provider. Review the privacy policy of the service you choose. Local models can process requests on your own computer. The mod itself NEVER collects any data, nor does it have any connection to a "SentientSands server". So any data collection that may happen is between you and your chosen LLM provider.

SUPPORT AND COMMUNITY
SentientSands Kayak is an experimental mod combining Kenshi, native game hooks, Python services and rapidly evolving AI models. Different hardware, providers and mod combinations may produce different results.
For installation help, configuration advice, model recommendations, bug reports, modding discussions or general questions, join our Discord:
https://discord.com/channels/1527415749172265080/1527415749772185662
