# O que eu aprendi sobre AWS Step Functions
## Introdução
Recentemente, comecei a estudar o AWS Step Functions com o curso engenharia de prompt da dio.me e queria compartilhar um pouco sobre o que aprendi sobre esse serviço, como ele funciona e algumas coisas interessantes que descobri durante o processo.

## O que é o Step Functions?
O AWS Step Functions é um serviço da AWS que facilita a coordenação de vários serviços, como AWS Lambda, em fluxos de trabalho visuais. Ele permite orquestrar tarefas e definir sequências de execução de uma maneira bem clara e estruturada. O que é interessante aqui é que você pode criar fluxos que tratam desde a execução de scripts simples até processos complexos e longos.

## Tipos de Workflows
Uma coisa que eu achei legal é que o Step Functions oferece dois tipos de workflows:

**Standard Workflows**: Esses são indicados para execuções de longa duração, podendo durar até 1 ano. Eles garantem uma alta resiliência, o que significa que você pode recuperar processos em caso de falhas e ter um histórico detalhado de cada passo.

**Express Workflows**: São mais adequados para fluxos de trabalho rápidos e de grande volume. O custo aqui é mais baixo se você precisa de alta escala, mas não é o ideal para processos longos. Além disso, a quantidade de detalhes no monitoramento é um pouco reduzida, comparado com os workflows padrão.

## Amazon States Language (ASL)
Para definir esses fluxos de trabalho, o Step Functions usa uma linguagem chamada <em>Amazon States Language (ASL)</em>. Ela é baseada em JSON e, no começo, pareceu meio técnica para mim, mas com o tempo comecei a entender melhor. O ASL define o que cada estado do fluxo faz, como as transições ocorrem, quais são os estados iniciais e finais, entre outras coisas.

Os estados podem fazer coisas como:

Executar tarefas: Por exemplo, chamar uma função Lambda.
Tomar decisões: Você pode configurar transições condicionais, o famoso "se isso, faça aquilo".
Esperar por determinado tempo: Tem um estado "Wait" que literalmente pausa a execução por um período que você definir.
A sintaxe da ASL lembra bastante o JSON, então foi fácil me adaptar. Exemplo básico de uma definição em ASL:

<code>
{
  "StartAt": "PrimeiroEstado",
  "States": {
    "PrimeiroEstado": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:MeuLambda",
      "Next": "SegundoEstado"
    },
    "SegundoEstado": {
      "Type": "Succeed"
    }
  }
}
</code>

## O que mais achei interessante?
O que eu mais gostei no Step Functions é que ele me dá uma visão gráfica de todo o fluxo de trabalho. Eu consigo ver exatamente em qual parte do fluxo está ocorrendo a execução, o que facilita bastante o debug e a análise de falhas e também a fácil integração com outros serviços da AWS.

