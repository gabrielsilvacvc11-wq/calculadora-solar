# Calculadora Solar · YWS

Site de uma página só, feito para o celular. Você digita quanto o cliente paga de luz por mês e ele mostra quantos painéis, quantos kWp e quantos kWh por mês a usina geraria, além de como o sol se comporta na cidade dele.

Não precisa instalar nada. É um único arquivo: `calculadora-solar.html`.

## O que mostra

- **Quantidade de painéis**, em destaque.
- **Usina em kWp** e **geração por mês em kWh**.
- **Consumo estimado**, **área no telhado** e **economia estimada por mês**.
- **Como o sol age na cidade**: altura do sol ao longo do dia em dezembro, março/setembro e junho, com a duração do dia, a direção e a inclinação ideais dos painéis, e a geração mês a mês.
- Uma faixa fixa no topo com o resultado, que aparece quando o número grande sai da tela.

## Como usar

1. Digite o valor da conta de luz (R$ por mês).
2. Escolha o tipo de ligação (monofásica, bifásica ou trifásica).
3. Escolha a cidade do cliente.
4. Se precisar, abra **Ajustar tarifa, sol e painel** e mude os valores.

## Como o cálculo funciona

1. Consumo (kWh) = valor da conta ÷ tarifa.
2. Desconta a taxa mínima: 30 kWh (mono), 50 kWh (bi) ou 100 kWh (tri).
3. kWp necessário = consumo a compensar ÷ (horas de sol pleno × 30 dias × eficiência).
4. Painéis = kWp × 1000 ÷ potência do painel, arredondado para cima.
5. Geração = kWp real da usina × horas de sol pleno × 30 × eficiência.
6. Economia = geração × tarifa, limitada ao consumo a compensar.
7. Área = painéis × 1,14 m × 2,40 m (medida de um painel de 610 W).

## Valores iniciais

| Campo | Valor inicial | Observação |
| --- | --- | --- |
| Tarifa | R$ 1,00 por kWh | Confira na conta do cliente (TE + TUSD com impostos). Muda todo ano. |
| Sol pleno | 5,4 h por dia | Média aproximada para Goiás. Ajuste se tiver o dado da cidade. |
| Eficiência | 80% | Perdas de inversor, cabos, temperatura e sujeira. |
| Painel | 610 W | Mude se for vender outro modelo. |

Para mudar os valores iniciais, procure no HTML os campos `id="tar"`, `id="hsp"`, `id="pr"` e `id="w"` e troque o `value`.

## Limites importantes

- É uma **estimativa inicial** para conversar com o cliente. O projeto final depende da visita técnica, do telhado e das sombras.
- A **altura do sol e a duração do dia** são cálculo astronômico pela latitude da cidade.
- A **variação mês a mês** usa um perfil típico do Centro-Oeste, com mais chuva de novembro a março. Não é medição. Para números oficiais, use os dados de irradiação do CRESESB.
- As cidades da lista têm só a latitude. O sol pleno é o mesmo campo para todas.
- A taxa mínima continua sendo cobrada na conta.

## Como colocar no ar

**Vercel ou GitHub Pages**

1. Crie um repositório no GitHub e suba o `calculadora-solar.html` renomeado para `index.html`.
2. Na Vercel, importe o repositório. Como é HTML puro, não precisa de nenhuma configuração.
3. Para usar um endereço da empresa, adicione o domínio nas configurações do projeto na Vercel.

**Direto no celular**

Mande o arquivo por WhatsApp e abra no navegador, ou hospede em qualquer lugar que sirva HTML.

## Como adicionar uma cidade

No HTML, dentro do `<select id="cid">`, adicione uma linha com a latitude (sem o sinal de menos):

```html
<option value="17.80">Rio Verde</option>
```

## Detalhes técnicos

- HTML, CSS e JavaScript puros, sem dependências.
- Fontes do Google Fonts (Bricolage Grotesque e Figtree), com fonte padrão do sistema como reserva.
- Tema claro e escuro automático, conforme o celular.
- Funciona sem internet, exceto pelas fontes.
