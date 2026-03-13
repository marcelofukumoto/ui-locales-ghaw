# pt-br Translation Learnings

Run 3 (2026-03-13): 89.78% -> 90.33% (35 new strings, 6348 total keys)

Cross-fork push fix: git remote set-url origin https://github.com/MYoshi/ui-locales-ghaw.git; git fetch origin pt-br-test-flow

Top untranslated (mostly legitimately identical): cluster(118), typeLabel(70), logging(42), fleet(33)

Already-translated ICU plurals: fleet.application, fleet.helmop, limitrange, resourcequota, poddisruptionbudget, servicemonitor, podmonitor, prometheusrule, thanosruler, alertmanagerconfig, cluster.x-k8s.io (Cluster CAPI), oidcclient (App OIDC)

YAML: js-yaml strips comments. Use extractLeafPaths() for dotted-key types. isNonTranslatable: add refresh/error/checkmark/time units.

PT-BR: Dashboard=Painel, Login=Entrar, Download=Baixar, Plugins=Extensoes, Core=Nucleo, English=Ingles, App Bundles=Pacotes de App, Autoscaler=Autoescalador, Network Policy=Politica de Rede, restricted=restrito
