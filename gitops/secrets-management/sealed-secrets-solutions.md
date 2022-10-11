## Teste

## Sealed Secrets:
  - Menor escala.
  - Cada secret tem que ser encriptados manualmente.
  - As chaves de encriptação/decriptação estão localizadas no namespace do controller do Sealed Secrets.

## Argo CD Vault Plugin:
  - Não é instalado no cluster e sim no Argo CD, é um plugin que pega os secrets de Secrets Managers externos (da AWS por exemplo).
  - Como é um plugin do Argo CD, esse não terá um CRD ou Controller no cluster.

## SOPS (Secrets OPerationS):
  - Não é mais usado desde 2018.
  - Imagine que o Sealed Secrets e o Argo CD Vault Plugin tiveram um bebê, esse é o SOPS!
    - O que ele puxou do Sealed Secrets é que cada secret tem que ser gerado manualmente.
    - O que ele puxou do Argo CD Vault Plugin é que algo é guardo externo ao cluster, mas dessa vez não são os secrets em si, mas as chaves de encriptação/decriptação.
    - Outra coisa que  ele puxou do Argo CD Vault Plugin é que ele é um plugin, logo não é instalado diretamente no cluster.

## Vault Agent:
  - Dispensa o uso de secrets.
  - É possível fazer atualizações de secretes on-fly.
  - Cada pod terá um agent responsável por conectá-lo ao Vault, ou seja, caso você tenha um milhão de pods, você terá um milhão de agents, ou seja a escalabilidade morreu.

## Secret Store CSI:
  - Dispensa o uso de secrets.
  - NÃO é possível fazer atualizações de secretes on-fly.
  - Cada node terá um CSI Driver que monta os secrets nos pods.
  - Os secrets são puxados de Secrets Managers externos (da AWS por exemplo).

## External Secrets:
  - Me parece que é basicamente o Argo CD Vault Plugins mas instalado diretamente no cluster.
  - Se você não tem tempo ou está indeciso, vai de External Secrets!!
