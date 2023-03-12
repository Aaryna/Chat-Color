# Chat-Color
import org.bukkit.ChatColor;
import org.bukkit.command.Command;
import org.bukkit.command.CommandSender;
import org.bukkit.entity.Player;
import org.bukkit.plugin.java.JavaPlugin;

public class ChatColorPlugin extends JavaPlugin {

@OverRide
public void onEnable() {
getLogger().info("ChatColorPlugin enabled");
}

@OverRide
public void onDisable() {
getLogger().info("ChatColorPlugin disabled");
}

@OverRide
public boolean onCommand(CommandSender sender, Command cmd, String label, String[] args) {
if (cmd.getName().equalsIgnoreCase("color") && sender instanceof Player) {
Player player = (Player) sender;
if (args.length > 0) {
ChatColor color = getChatColor(args[0]);
if (color != null) {
player.setDisplayName(color + player.getName());
player.sendMessage("Your chat color has been changed to " + color + args[0]);
return true;
}
else if (args[0].startsWith("#")) {
ChatColor hexColor = getHexColor(args[0]);
if (hexColor != null) {
player.setDisplayName(hexColor + player.getName());
player.sendMessage("Your chat color has been changed to " + hexColor + args[0]);
return true;
}
}
}
sendValidColorsMessage(player);
return true;
}
return false;
}

private ChatColor getChatColor(String colorName) {
try {
return ChatColor.valueOf(colorName.toUpperCase());
} catch (IllegalArgumentException e) {
return null;
}
}

private ChatColor getHexColor(String hexColor) {
try {
String hexString = hexColor.substring(1);
int rgb = Integer.parseInt(hexString, 16);
return ChatColor.of(new java.awt.Color(rgb));
} catch (IllegalArgumentException e) {
return null;
}
}

private void sendValidColorsMessage(Player player) {
player.sendMessage("Valid colors: " + ChatColor.BLACK + "black, " + ChatColor.DARK_BLUE + "dark_blue, " +
ChatColor.DARK_GREEN + "dark_green, " + ChatColor.DARK_AQUA + "dark_aqua, " +
ChatColor.DARK_RED + "dark_red, " + ChatColor.DARK_PURPLE + "dark_purple, " +
ChatColor.GOLD + "gold, " + ChatColor.GRAY + "gray, " + ChatColor.DARK_GRAY + "dark_gray, " +
ChatColor.BLUE + "blue, " + ChatColor.GREEN + "green, " + ChatColor.AQUA + "aqua, " +
ChatColor.RED + "red, " + ChatColor.LIGHT_PURPLE + "light_purple, " + ChatColor.YELLOW + "yellow, " +
ChatColor.WHITE + "white");
player.sendMessage("You can also use hex colors by specifying a color code starting with #, e.g. " + ChatColor.WHITE + "#FF0000");
}
}

