# UNION - Documento de Design do Servidor RP

## Visão Geral
UNION é um servidor RP americano na FiveM com foco em mundo vivo, autônomo e infinito. O RP surge de sistemas invisíveis: a cidade reage, lembra e esquece. Não há dependência de eventos administrativos para gerar narrativa.

**Regras de ouro**
- Nada de sistemas mágicos.
- Nada de UI explicando tudo.
- Nada de RP forçado por admin.
- O mundo deve reagir, lembrar e esquecer.
- O RP deve emergir naturalmente.

## Identidade Visual
- Nome: **UNION**.
- Estilo: urbano, realista, industrial.
- Entregáveis visuais:
  - Logo.
  - Loadscreen.
  - HUD personalizado.
  - Celular e tablet customizados.
  - Inventário limpo, sem UI chamativa ou arcade.

## Economia e Vida Legal
### Empregos iniciais (acessíveis)
- Entregador local.
- Gari urbano.
- Motorista de carga leve.
- Auxiliar de depósito.

### Profissões essenciais
- Polícia.
- Hospital.
- Mecânica.

### Regras da Mecânica
- Mecânica realiza apenas reparos: motor, pneus, lataria.
- Jogadores comuns podem comprar:
  - Até 3 pneus.
  - Até 3 kits de ferramenta.
- Kits de ferramenta:
  - Recuperam 30%–45% do motor.
  - Limitados a 80% de integridade.
  - Itens de uso único.
- Apenas mecânicos em serviço podem restaurar 100%.
- Se houver **5+ mecânicos em serviço**, a bancada de ferramentas é desativada.
- Se houver **4 ou menos**, a bancada fica ativa para compra autônoma.
- Mecânicos fora de serviço são tratados como jogadores comuns.

## Sistema Médico
### Itens
- Analgésicos: reduzem sangramento e aumentam stamina por curto período.
- Bandagens: estancam sangramento.
- Kits médicos: curam 25%–35% (uso único), limitados a 65% de vida.

### Limites por jogador
- 5 analgésicos.
- 6 bandagens.
- 3 kits médicos.

### Restrição de cura
Ao atingir o limite de cura permitido por item, apenas o hospital pode restaurar totalmente.

## Inventário Físico
- Inventário com **slots** e **peso máximo**.
- Jogadores começam com inventário limitado.
- Aumentos somente via item consumível **"mochila"**:
  - Aumenta slots e peso.
  - Limitado a 8 usos.
  - Não é a mochila estética.
- Porta-malas e porta-luvas com inventários próprios.
- Peso sempre relevante; nenhum item pesa zero.

## Itens de Comunicação (Obrigatório)
### Celular (item físico)
- Sem celular: sem chamadas, mensagens, apps ou banco.
- O número pertence ao item, não ao personagem.
- Pode ser roubado, perdido ou apreendido.
- Sons de notificação são audíveis para jogadores próximos (som 3D).

### Rádio (item físico)
- Comunicação de grupo por frequência.
- Pode ser apreendido.
- Rádio criptografado existe, mas nunca é 100% seguro.
- Comunicação só funciona se o item estiver no inventário.

## Mundo Ilegal Interdependente
- Gangues de drogas.
- Organizações de armas.
- Grupo de roubo e desmanche de veículos.
- Logística e contrabando.
- Nenhuma organização é totalmente independente.
- Organizações do mesmo segmento **não cooperam** entre si.

### Cadeias de insumo
- Materiais do desmanche servem como insumo para:
  - Tuning ilegal.
  - Fabricação de armas.
  - Processos químicos (ex: ácido de bateria).
- Tuning ilegal usa peças recicladas.
- Ajustes corretos melhoram o carro; ajustes errados pioram.

## Sistemas Vivos (Núcleo do Servidor)
### World Memory
- Regiões acumulam “calor” conforme eventos (crime, tiros, overdoses).
- A memória decai com o tempo.
- Afeta comportamento de NPCs, serviços e polícia.
- Nunca é mostrada ao jogador.

### Histórias Não Escritas
- Eventos raros criam ecos narrativos.
- NPCs e serviços reagem de forma sutil.
- Histórias surgem e desaparecem com o tempo.

### Auto Balance
- Atividades dominantes se tornam menos vantajosas.
- Atividades abandonadas se tornam mais atrativas.
- Ajustes são lentos, invisíveis e nunca anunciados.

## Sistemas de Lazer
- Corridas ilegais gerenciadas por grupos ilegais.
- Sistema de remap:
  - Ajustes finos.
  - Não transforma carros em supermáquinas.
  - Erro gera piora de performance.

## Sistemas de Vida
- Fome.
- Sede.
- Stamina.
- Fadiga.
- Consumo de alimentos e bebidas é necessário para sobrevivência.
- Produtos específicos lidam com fadiga.

## Arquitetura
- Base própria.
- Organização clara em pastas separadas por seção.
- Banco de dados completo, normalizado, com suporte a metadata.
- `server.cfg` pronto para produção.

### Organização de pastas (proposta)
```
resources/
  [core]/
    union-base/
    union-inventory/
    union-jobs/
    union-medical/
    union-vehicles/
  [world]/
    union-world-memory/
    union-narratives/
    union-autobalance/
  [illegal]/
    union-drugs/
    union-arms/
    union-chopshop/
    union-smuggling/
  [ui]/
    union-hud/
    union-phone/
    union-tablet/
  [assets]/
    union-logo/
    union-loadscreen/
config/
  server.cfg
  permissions.cfg
  logging.cfg
  economy.cfg
  inventory.cfg
  medical.cfg
  communication.cfg
  world.cfg
  illegal.cfg
  leisure.cfg
  needs.cfg
  vehicles.cfg
  tuning.cfg
  balance.cfg
  identity.cfg
  jobs.cfg
  police.cfg
  hospital.cfg
  mechanic.cfg
  database.cfg
```

## Regras de Balanceamento Inicial
- Economia com progressão lenta, foco em consumo diário.
- Itens raros sempre exigem cadeia de insumos ilegais ou logística.
- Jobs iniciais mantêm o jogador funcional sem gerar riqueza rápida.

## Logs e Auditoria
- Logs econômicos detalhados (entrada/saída de dinheiro e itens).
- Auditoria por profissões essenciais e sistemas ilegais.
- Ações críticas registradas sem expor UI aos jogadores.

## Observações de Implementação
- UI deve comunicar estado via elementos diegéticos (sons, notificações discretas, feedback de mundo).
- Telefone, rádio, kits e mochilas devem existir como itens físicos com peso.
- Scripts devem preferir reações indiretas do mundo (ex: NPCs mudando rotina) ao invés de avisos explícitos.
