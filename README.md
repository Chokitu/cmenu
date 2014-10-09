#include <sourcemod>
#include <sdktools>
#include <cstrike>
#include <colors>

#define PLUGIN_VERSION  "1.0"

public Plugin:myinfo = {
        name = "Warden - Menu",
        author = "Killer Boy",
        version = PLUGIN_VERSION,
        description = "Warden - menu",
};

public OnPluginStart()
{ 
	RegConsoleCmd("brincar", Afficher_Menu_Bhop);
	HookEvent("player_spawn", OnPlayerSpawn);
}

public Action:OnPlayerSpawn(Handle:event, const String:name[], bool:dontBroadcast)
{
	new client = GetClientOfUserId(GetEventInt(event, "userid"));
	CPrintToChat(client, "");
}

public Action:Afficher_Menu_Bhop(client, args)
{
	if(GetClientTeam(client) == 3) //number 3 means that if hes a counter terrorist.
	{ // So this code is execly for CT
		new Handle:menu = CreateMenu(bhopvip);
		SetMenuTitle(menu, "Menu De Brincadeiras");
		AddMenuItem(menu, "option1", "FreeDay");
		AddMenuItem(menu, "option2", "Pega-Pega");
		AddMenuItem(menu, "option3", "Esconde-Esconde");
		AddMenuItem(menu, "option4", "Box"
		SetMenuExitButton(menu, true);
		DisplayMenu(menu, client, MENU_TIME_1);
	}
	else
	{ //This code is execly for T Side, the spectators side would be 1, but I think would be useless to use a command on spectators.
		PrintToChat(client, "You are not in team CT");
	}
	return Plugin_Handled; 
}

public bhopvip(Handle:menu, MenuAction:action, client, itemNum)
{
	if ( action == MenuAction_Select )
	{
		switch (itemNum)
		{
			case 0:
			{
				FakeClientCommand(client, "say /free");
			}
			case 1:
			{
			    FakeClientCommand(client, "say /abrir");
				FakeClientCommand(client, "say !slap @t 99");
				FakeClientCommand(client, "say PEGA-PEGA, TR SÓ PODE MATAR CT COM FACA");
			}
			case 2:
			{
			    FakeClientCommand(client, "say /abrir");
				FakeClientCommand(client, "say !gravity @all 0.3");
				FakeClientCommand(client, "say !freeze c 50"
				FakeClientCommand(client, "say ESCONDE-ESCONDE, CT VAI FICAR PARADO NA BASE congelado, quando sair do congelado ele vai procurar os Terroristas, que só podem patar ele com arma depois do relogio estar no 3:00 antes só com faca");
			}
			case 3:
			{
			    FakeClientCommand(client, "say /box");
				FakeClientCommand(client, "say !abrir"
				FakeClientCommand(client, "say Tr's tentam se matar,se matar CT é ban, quem sobrar da LR"
			}
		}
	}
	else if (action == MenuAction_End )
	{
	CloseHandle(menu);
	} 
}
