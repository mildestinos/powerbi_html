PainelMapa_Pro_HTML = 
VAR Pais = [EmojiPais]
VAR Receita = [ReceitaAtual]
VAR ReceitaPct = [VarPctReceita]
VAR Lucro = [LucroAtual]
VAR LucroPct = [VarPctLucro]
VAR ProdutoTop = 
    CALCULATE(
        MAX(financials[Product]),
        TOPN(1, SUMMARIZE(financials, financials[Product], "V", SUM(financials[Sales])), [V], DESC)
    )
VAR SegmentoTop = 
    CALCULATE(
        MAX(financials[Segment]),
        TOPN(1, SUMMARIZE(financials, financials[Segment], "V", SUM(financials[Sales])), [V], DESC)
    )
VAR BarrasProdutos = [GraficoTop3Produtos]

VAR IconeReceita = IF(ReceitaPct >= 0, "▲", "▼")
VAR IconeLucro = IF(LucroPct >= 0, "▲", "▼")

RETURN
"
<div style='font-family:Segoe UI,sans-serif; padding:16px; max-width:900px; margin:auto;'>
  <h2 style='margin-bottom:12px;'>Indicadores do país: " & Pais & "</h2>

  <div style='display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:12px;'>

    <div style='background:#1e3a8a; color:white; border-radius:10px; padding:14px;'>
      <div style='font-size:13px;'>Receita</div>
      <div style='font-size:20px; font-weight:bold;'>R$ " & FORMAT(Receita, "#,##0.00") & "</div>
      <div style='font-size:12px;'> " & IconeReceita & " " & FORMAT(ReceitaPct, "0.0%") & " vs mês anterior</div>
    </div>

    <div style='background:#047857; color:white; border-radius:10px; padding:14px;'>
      <div style='font-size:13px;'>Lucro</div>
      <div style='font-size:20px; font-weight:bold;'>R$ " & FORMAT(Lucro, "#,##0.00") & "</div>
      <div style='font-size:12px;'> " & IconeLucro & " " & FORMAT(LucroPct, "0.0%") & " vs mês anterior</div>
    </div>

    <div style='background:#facc15; color:#1e293b; border-radius:10px; padding:14px;'>
      <div style='font-size:13px;'>Produto Mais Vendido</div>
      <div style='font-size:18px; font-weight:bold;'>" & ProdutoTop & "</div>
    </div>

    <div style='background:#e2e8f0; color:#1e293b; border-radius:10px; padding:14px;'>
      <div style='font-size:13px;'>Segmento Principal</div>
      <div style='font-size:18px; font-weight:bold;'>" & SegmentoTop & "</div>
    </div>
  </div>

  <div style='margin-top:24px;'>
    <h3 style='font-size:16px; margin-bottom:6px;'>Top 3 produtos</h3>
    " & BarrasProdutos & "
  </div>
</div>
"
