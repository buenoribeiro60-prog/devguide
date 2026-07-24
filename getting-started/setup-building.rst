# ==============================================
 #               A4HFF4X - SISTEMA PRONTO
 # ==============================================
 import time
 import random
 a4hff4x = {
     "ativo": False,
     "modo": "peito_para_cabeca",
     "forca": 10,
     "velocidade": 95,
     "anti_ban": True,
     "anti_blacklist": True
 }
 def mira_alvo(pos_peito):
     if not a4hff4x["ativo"]:
         return pos_peito
     print(f"🔫 Mira no peito: {pos_peito}")
     time.sleep(random.uniform(0.02, 0.06))
     ajuste = (a4hff4x["forca"] * 4) * (a4hff4x["velocidade"] / 100)
     pos_cabeca = pos_peito - 40
     mira_final = pos_peito - ajuste
     if mira_final < pos_cabeca: mira_final = pos_cabeca
     print(f"🎯 Mira na cabeça: {round(mira_final, 2)}")
     return mira_final
 def comando(cmd):
     cmd = cmd.lower().strip()
     if cmd == "/a4hff4x on":
         a4hff4x["ativo"] = True
         return "✅ A4HFF4X LIGADO | MODO HÃ HÃ PAI"
     elif cmd == "/a4hff4x off":
         a4hff4x["ativo"] = False
         return "❌ DESLIGADO"
     elif cmd == "/status":
         return f"""
 📊 STATUS:
 ✅ Ativo: {a4hff4x['ativo']}
 💪 Força: {a4hff4x['forca']}
 🛡️ Proteção: {a4hff4x['anti_ban']}
         """
     elif cmd == "sair": return "🔌 FECHANDO..."
     else: return "❌ Comando inválido"
 if __name__ == "__main__":
     print("="*35)
     print("      A4HFF4X - PRONTO PRA USAR")
     print("="*35)
     while True:
         digite = input("> ")
         print(comando(digite))
         if digite == "sair": break
         if a4hff4x["ativo"]: mira_alvo(920)
