import discord
from discord.ext import commands
import random

# Configuração
intents = discord.Intents.default()
intents.message_content = True

bot = commands.Bot(command_prefix='$', intents=intents)

# Evento de inicialização
@bot.event
async def on_ready():
    print(f' EcoBot está online como {bot.user}!')

# Comando de apresentação
@bot.command()
async def hello(ctx):
    await ctx.send(f"Olá! Eu sou o {bot.user}! Meu objetivo é te ajudar a cuidar do planeta. Use $dica, $desafio, $reciclar ou $eco!")
# Lista de dicas ecológicas
dicas = [
    "Use garrafa reutilizável em vez de plástico.",
    "Desligue aparelhos da tomada quando não estiver usando.",
    "Evite desperdício de água.",
    "Use sacolas reutilizáveis.",
    "Prefira produtos sustentáveis.",
    "Recicle sempre que possível."
]

# Comando de dica
@bot.command()
async def dica(ctx):
    await ctx.send(f"Dica ecológica: {random.choice(dicas)}")

# Lista de desafios
desafios = [
    "Fique um dia sem usar plástico!",
    "Recicle todo o lixo hoje.",
    "Economize água no banho.",
    "Evite produtos descartáveis hoje.",
    "Reutilize algo em casa."
]

# Comando de desafio
@bot.command()
async def desafio(ctx):
    await ctx.send(f" Desafio ecológico: {random.choice(desafios)}")

# Reciclagem
reciclagem = {
    "papel": " Papel → lixeira azul.",
    "plastico": " Plástico → lixeira vermelha.",
    "vidro": " Vidro → lixeira verde.",
    "metal": " Metal → lixeira amarela."
}

# Comando reciclar
@bot.command()
async def reciclar(ctx, item: str = None):
    if item is None:
        await ctx.send("Use assim: $reciclar papel/plastico/vidro/metal")
        return

    item = item.lower()
    if item in reciclagem:
        await ctx.send(reciclagem[item])
    else:
        await ctx.send("Não conheço esse material. Use: papel, plastico, vidro ou metal.")
# Comando extra educativo
@bot.command()
async def eco(ctx):
    mensagens = [
        " Pequenas atitudes fazem grande diferença!",
        " Reciclar ajuda a reduzir a poluição!",
        " Cuidar do planeta é responsabilidade de todos!",
        " Sustentabilidade começa com você!"
    ]
    await ctx.send(random.choice(mensagens))
