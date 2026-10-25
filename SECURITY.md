# Segurança / Security

Encontrou uma vulnerabilidade na API, no painel ou nestes repositórios? Escreva para **contato@luniumpay.com** com assunto `[security]`. Respondemos a reportes responsáveis, não processamos quem reporta de boa-fé e combinamos a divulgação. Não publique detalhes em issues.

Found a vulnerability? E-mail **contato@luniumpay.com** with subject `[security]`. We acknowledge responsible reports and coordinate disclosure. Please do not open public issues for security matters.

Regras que valem para todo integrador: chaves `lun_live_` e `webhook_secret` só em variáveis de ambiente do servidor; valide a assinatura dos webhooks sobre o corpo cru; nunca exponha o `monitor_url`.
