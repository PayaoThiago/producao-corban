export default function handler(req, res) {
  const intent = req.body.queryResult?.intent.displayName;
  const params = req.body.queryResult?.parameters || {};

  let resposta = 'Desculpe, não consegui entender.';

  if (intent === 'Produção Corban') {
    const correspondente = params['correspondente'] || 'NÃO INFORMADO';

    const producoes = {
      BEVICRED: 'R$ 182.000',
      LEWE: 'R$ 75.400',
      ITS: 'R$ 101.000'
    };

    const producao = producoes[correspondente.toUpperCase()] || 'sem produção registrada';
    resposta = `📊 Produção da ${correspondente} hoje: ${producao}`;
  }

  res.status(200).json({ fulfillmentText: resposta });
}