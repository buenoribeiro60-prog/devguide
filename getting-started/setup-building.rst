# ==============================================
#               A4HFF4X - SISTEMA FFHX
#               VERSÃO PYTHON COMPLETA
# ==============================================

import time
import random

# CONFIGURAÇÕES PRONTAS
a4hff4x = {
    "ativo": False,
    "modo": "peito_para_cabeca",
    "forca": 10,
    "velocidade": 95,
    "recuo": "zero",
    "anti_ban": True,
    "anti_blacklist": True,
    "furtivo": True
}

# FUNÇÃO DA MIRA
def mira_alvo(pos_peito):
    if not a4hff4x["ativo"]:
        return pos_peito

    print(f"🔫 Mira no peito: {pos_peito}")
    
    if a4hff4x["anti_ban"]:
        time.sleep(random.uniform(0.02, 0.06))

    ajuste = (a4hff4x["forca"] * 4) * (a4hff4x["velocidade"] / 100)
    pos_cabeca = pos_peito - 40
    mira_final = pos_peito - ajuste
    
    if mira_final < pos_cabeca:
        mira_final = pos_cabeca

    print(f"🎯 Mira na cabeça: {round(mira_final, 2)}")
    return mira_final

# COMANDOS
def comando(cmd):
    cmd = cmd.lower().strip()

    if cmd == "/a4hff4x on":
        a4hff4x["ativo"] = True
        return "✅ A4HFF4X LIGADO | MODO HÃ HÃ PAI"
    
    elif cmd == "/a4hff4x off":
        a4hff4x["ativo"] = False
        return "❌ DESLIGADO"
    
    elif cmd == "/modo peito_cabeca":
        a4hff4x["modo"] = "peito_para_cabeca"
        return "🎯 MODO: PEITO → CABEÇA"
    
    elif cmd == "/forca max":
        a4hff4x["forca"] = 10
        return "💪 FORÇA MÁXIMA"
    
    elif cmd == "/protecao total":
        a4hff4x["anti_ban"] = True
        a4hff4x["anti_blacklist"] = True
        return "🛡️ PROTEÇÃO TOTAL LIGADA"
    
    elif cmd == "/status":
        return f"""
📊 STATUS A4HFF4X:
✅ Ativo: {a4hff4x['ativo']}
🎯 Modo: {a4hff4x['modo']}
💪 Força: {a4hff4x['forca']}
🛡️ Anti-Ban: {a4hff4x['anti_ban']}
        """
    
    elif cmd == "sair":
        return "🔌 FECHANDO..."
    
    else:
        return "❌ Comando inválido"

# INICIO
if __name__ == "__main__":
    print("=" * 35)
    print("      A4HFF4X - PRONTO PRA USAR")
    print("=" * 35)
    print("Comandos: /a4hff4x on | /status | /sair\n")

    while True:
        digite = input("> ")
        res = comando(digite)
        print(res)
        
        if digite == "sair":
            break
        
        if a4hff4x["ativo"]:
            print("\n🎯 TESTE:")
            mira_alvo(920)
            print("-" * 35)
