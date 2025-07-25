import discord
import openai
from discord.ext import commands

# ⚠️ WARNING: Hardcoded keys – not safe for public use
TOKEN = "sk-MTM4MzY5OTI0Mzk1MjUwODk1OQ.GI_lH4.frvy_NQFh2R4DcyaVZs-cic55x_0sliUoH5uDo"
OPENAI_API_KEY = "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"

openai.api_key = OPENAI_API_KEY

intents = discord.Intents.default()
intents.message_content = True
bot = commands.Bot(command_prefix="/", intents=intents)

@bot.event
async def on_ready():
    print(f"✅ Logged in as {bot.user}")

@bot.command()
async def tip(ctx):
    await ctx.send("📈 Forex Tip: Always manage your risk, never overleverage!")

@bot.command()
async def affirmation(ctx):
    await ctx.send("🧠 Affirmation: I am focused, aligned, and financially unstoppable.")

@bot.command()
async def ask(ctx, *, question):
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": question}]
    )
    await ctx.send(response['choices'][0]['message']['content'])

bot.run(TOKEN)
