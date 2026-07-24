# ==============================================
#           FFHX - MODO HÃ HÃ PAI 🤙
#       VERSÃO COMPLETA + ANTI-BAN / ANTI-BLACKLIST
# ==============================================

import time
import random

# CONFIGURAÇÕES GERAIS
ffhx = {
    "ativo": False,
    "modo": "peito_para_cabeca",
    "forca": 5,
    "velocidade": 50,
    "recuo": "normal",
    "trava_alvo": False,
    "tipo_movimento": "suave",
    
    # SISTEMA DE SEGURANÇA
    "anti_ban": False,
    "anti_blacklist": False,
    "modo_furtivo": False,
    "evasao_deteccao": False,
    "delay_aleatorio": True,
    "limite_ajustes": True,
    "ocultar_atividade": False
}

# ==============================================
# FUNÇÃO DE AJUSTE DA MIRA (PEITO → CABEÇA)
# ==============================================
def ajustar_mira(posicao_peito):
    if not ffhx["ativo"]:
        return posicao_peito
    
    # APLICA PROTEÇÕES SE ESTIVER ATIVO
    if ffhx["anti_ban"] and ffhx["delay_aleatorio"]:
        time.sleep(random.uniform(0.02, 0.08)) # Pequeno atraso para parecer humano
    
    print(f"🔫 Mira no peito: {posicao_peito}")
    
    if ffhx["modo"] == "peito_para_cabeca":
        ajuste = (ffhx["forca"] * 4) * (ffhx["velocidade"] / 100)
        posicao_cabeca = posicao_peito - 40
        mira_final = posicao_peito - ajuste
        
        # Limita ajustes para não exagerar (anti-deteccao)
        if ffhx["limite_ajustes"]:
            ajuste_max = 45
            if (posicao_peito - mira_final) > ajuste_max:
                mira_final = posicao_peito - ajuste_max
        
        if mira_final < posicao_cabeca:
            mira_final = posicao_cabeca
        print(f"🎯 Subiu para cabeça: {round(mira_final, 2)}")
        return mira_final

    elif ffhx["modo"] == "so_peito":
        print("🎯 Mira fixa no peito")
        return posicao_peito

    elif ffhx["modo"] == "so_cabeca":
        mira_final = posicao_peito - 35
        print(f"🎯 Mira direto na cabeça: {mira_final}")
        return mira_final

    elif ffhx["modo"] == "pescoco_para_cabeca":
        ajuste = 15 + (ffhx["forca"] * 2)
        mira_final = posicao_peito - ajuste
        print(f"🎯 Pescoco → Cabeça: {mira_final}")
        return mira_final

# ==============================================
# SISTEMA DE TODOS OS COMANDOS
# ==============================================
def executar_comando(cmd):
    cmd = cmd.lower().strip()

    # ==============================================
    # COMANDOS GERAIS
    # ==============================================
    if cmd == "/ffhx on":
        ffhx["ativo"] = True
        return "✅ FFHX LIGADO | MODO HÃ HÃ PAI"
    elif cmd == "/ffhx off":
        ffhx["ativo"] = False
        return "❌ FFHX DESLIGADO"
    elif cmd == "/ffhx status":
        return f"""
📊 STATUS FFHX:
✅ Ativo: {ffhx['ativo']}
🎯 Modo: {ffhx['modo']}
💪 Força: {ffhx['forca']}/10
⚡ Velocidade: {ffhx['velocidade']}
🔫 Recuo: {ffhx['recuo']}
🔒 Trava alvo: {ffhx['trava_alvo']}

🛡️ SEGURANÇA:
✅ Anti-Ban: {ffhx['anti_ban']}
✅ Anti-Blacklist: {ffhx['anti_blacklist']}
✅ Modo Furtivo: {ffhx['modo_furtivo']}
        """
    elif cmd == "/ffhx versao":
        return "ℹ️ Versão: 1.1 + SEGURANÇA"
    elif cmd == "/ffhx ajuda":
        return "Digite: /ffhx on /modo /forca /anti-ban on /anti-blacklist on"

    # ==============================================
    # MODOS DE MIRA
    # ==============================================
    elif cmd == "/modo peito_para_cabeca":
        ffhx["modo"] = "peito_para_cabeca"
        return "🎯 MODO: PEITO → CABEÇA"
    elif cmd == "/modo so_peito":
        ffhx["modo"] = "so_peito"
        return "🎯 MODO: SÓ PEITO"
    elif cmd == "/modo so_cabeca":
        ffhx["modo"] = "so_cabeca"
        return "🎯 MODO: SÓ CABEÇA"
    elif cmd == "/modo pescoco_para_cabeca":
        ffhx["modo"] = "pescoco_para_cabeca"
        return "🎯 MODO: PESCOÇO → CABEÇA"
    elif cmd == "/modo misto":
        ffhx["modo"] = "misto"
        return "🎯 MODO: MISTO"
    elif cmd == "/modo livre":
        ffhx["modo"] = "livre"
        return "🎯 MODO: LIVRE"

    # ==============================================
    # FORÇA E VELOCIDADE
    # ==============================================
    elif cmd.startswith("/forca"):
        try:
            val = int(cmd.split()[1])
            ffhx["forca"] = max(1, min(10, val))
            return f"💪 Força: {val}/10"
        except: return "⚠️ Use: /forca 1 a 10"

    elif cmd.startswith("/velocidade") or cmd.startswith("/veloc"):
        try:
            val = int(cmd.split()[1])
            ffhx["velocidade"] = max(10, min(100, val))
            return f"⚡ Velocidade: {val}"
        except: return "⚠️ Use: /velocidade 10 a 100"

    # ==============================================
    # RECUO E MOVIMENTO
    # ==============================================
    elif cmd == "/recuo zero": ffhx["recuo"] = "zero"; return "🔫 RECUO ZERO"
    elif cmd == "/recuo medio": ffhx["recuo"] = "medio"; return "🔫 Recuo medio"
    elif cmd == "/recuo normal": ffhx["recuo"] = "normal"; return "🔫 Recuo normal"

    elif cmd == "/mira suave": ffhx["tipo_movimento"] = "suave"; return "🎯 Movimento suave"
    elif cmd == "/mira rapida": ffhx["tipo_movimento"] = "rapida"; return "🎯 Movimento rápido"

    # ==============================================
    # 🛡️ COMANDOS DE SEGURANÇA / ANTI-BAN / ANTI-BLACKLIST
    # ==============================================
    elif cmd == "/anti-ban on":
        ffhx["anti_ban"] = True
        ffhx["delay_aleatorio"] = True
        ffhx["limite_ajustes"] = True
        return "🛡️ ANTI-BAN ATIVADO ✅ | Proteção contra detecção"
    elif cmd == "/anti-ban off":
        ffhx["anti_ban"] = False
        return "🛡️ ANTI-BAN DESATIVADO ❌"

    elif cmd == "/anti-blacklist on":
        ffhx["anti_blacklist"] = True
        ffhx["evasao_deteccao"] = True
        ffhx["ocultar_atividade"] = True
        return "🛡️ ANTI-BLACKLIST ATIVADO ✅ | Não entra na lista negra"
    elif cmd == "/anti-blacklist off":
        ffhx["anti_blacklist"] = False
        return "🛡️ ANTI-BLACKLIST DESATIVADO ❌"

    elif cmd == "/modo furtivo on":
        ffhx["modo_furtivo"] = True
        return "🛡️ MODO FURTIVO LIGADO ✅ | Tudo parece natural"
    elif cmd == "/modo furtivo off":
        ffhx["modo_furtivo"] = False
        return "🛡️ MODO FURTIVO DESLIGADO ❌"

    elif cmd == "/protecao total":
        ffhx["anti_ban"] = True
        ffhx["anti_blacklist"] = True
        ffhx["modo_furtivo"] = True
        return "🛡️ PROTEÇÃO TOTAL ATIVADA ✅"

    elif cmd == "/reset protecao":
        ffhx["anti_ban"] = False
        ffhx["anti_blacklist"] = False
        ffhx["modo_furtivo"] = False
        return "🔄 Proteção resetada"

    # ==============================================
    # RESETS E OUTROS
    # ==============================================
    elif cmd == "/reset mira":
        ffhx["modo"] = "peito_para_cabeca"; ffhx["forca"] = 5; ffhx["velocidade"] = 50
        return "🔄 MIRA RESETADA"
    elif cmd == "/reset tudo":
        for chave in ffhx:
            if isinstance(ffhx[chave], bool): ffhx[chave] = False
            elif isinstance(ffhx[chave], int): ffhx[chave] = 50 if chave == "velocidade" else 5
            else: ffhx[chave] = "peito_para_cabeca" if chave == "modo" else "normal"
        return "🔄 TUDO RESETADO"

    elif cmd == "sair": return "🔌 Saindo..."
    else: return "❌ Comando inválido"

# ==============================================
# INICIO DO SISTEMA
# ==============================================
if __name__ == "__main__":
    print("=== FFHX SISTEMA + SEGURANÇA 🛡️🤙 ===")
    print("Digite comandos ou 'sair'\n")

    while True:
        cmd = input("> ")
        res = executar_comando(cmd)
        print(res)
        
        if cmd == "sair": break
        
        if cmd.startswith("/ffhx on") or cmd.startswith("/modo") or cmd.startswith("/anti-ban"):
            print("\n🎯 Teste:")
            ajustar_mira(920)
            print("-"*35)
