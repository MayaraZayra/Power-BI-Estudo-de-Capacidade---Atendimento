# Power-BI-Estudo-de-Capacidade---Atendimento
Painel com o estudo de capacidade necessário de colaboradores para atendimento x quantidade de chamados abertos (levando em consideração a produtividade)

TT CH Abertos = COUNTROWS(fChAbertos_Consolidado)
//Quantidade de chamados abertos,nessa medida verificamos o total de solitações por categoria/subcategoria, grupo de atribuição, área | Não há atualização no caso de reclassificação dos chamados, o objetivo é verificar a solicitação inicial.

Horário Abertura do Chamado = = Table.AddColumn(#"Tipo Alterado2", "Hora", each Time.Hour([Aberto]), Int64.Type) 
// Medida criada no Power Query -- Linguaguem M - Tranformar dados do Power BI: Coluna duplicada onde o formato foi alterado para hora. Neste caso tive que ajustar também o formato no Fluxo de dados do Power BI da base de chamados abertos, pois estava somente data.

Abertos DIA = [TT CH Aberto] / [Dias Úteis]
//Quantidade de chamados abertos por dias uteis

Dia da Semana (Nome) = SWITCH(
    'dCalendário'[Dia da Semana],
    0, "Dom",
    6, "Sáb",
    1,"Seg",
    2,"Ter",
    3,"Qua",
    4,"Qui",
    5,"Sex")
