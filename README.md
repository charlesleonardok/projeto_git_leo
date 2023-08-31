# projeto_git_leo
Aprendendo GIT Hub

## Título 02


AtendimentoMaster:
Load
    Text(fa) as AtendimentoId,
    Text(preferencial) as FlagAtendimentoPreferencial,
    Text(TipoAtendimentoId) as TipoAtendimentoId,
    Text(FormaAtendimentoId) as FormaAtendimentoId,
    Text(consumidor_id) as ConsumidorId,
    Text(TipoCategoriaId) as TipoCategoriaId,
    Num(DayName(data_hora_pre_atendimento)) as DataId,
    data_hora_pre_atendimento as DataHoraInicioPreAtendimento,
    data_hora as DataHoraInicioAtendimento,
    data_hora_fim_atendimento as DataHoraFimAtendimento,
    data_alteracao as DataHoraAlteracao,
    Ceil(Num(Interval(data_hora_fim_atendimento - data_hora)) * 1440) as TempoAtendimento,
    Ceil(Num(Interval(data_hora_fim_atendimento - data_hora_pre_atendimento)) * 1440) as TempoPreAtendimento,
    Text(identificacao_atendente) as Atendente,
    Text(procurou_empresa) as FlagProcurouEmpresa,
    Text(FormaContratacaoId) as FormaContratacaoId,
    Text(AreaId) as AreaId,
    Text(AreaNome) as AreaNome,
    Text(AssuntoId) as AssuntoId,
    Text(AssuntoNome) as AssuntoNome,
    Text(Text(DetalheProblemaId) & '|' & Text(DetalheProblemaItemId)) as DetalheProblemaId,
    Text(ProblemaNome) as ProblemaNome,
    Text(DetalheProblema) as DetalheProblemaItemNome,
    Text(status_atendimento) as StatusAtendimento,
    Text(foi_cancelado) as AtendimentoCancelado,
    Num(lotacao) as LocalId,
    Text(__KEY_resultado) as __KEY_resultado
Resident ConsultaAtendimento
Where
    Not IsNull(__KEY_resultado);

Join
Load
    Text(__FK_atendimento_fornecedores) as __KEY_resultado,
    Text(FornecedorId) as FornecedorId,
    Text(Fornecedor) as FornecedorNome,
    Text(ClassificacaoFornecedorId) as ClassificacaoFornecedorId,
    Text(ClassificacaoFornecedor) as ClassificacaoFornecedorNome
Resident ConsultaAtendimento
Where
    Not IsNull(__FK_atendimento_fornecedores);

Left Join (AtendimentoMaster)
Load
    Text(__FK_consumidor) as ConsumidorId,
    Text(ConsumidorTipo) as ConsumidorTipo,
    Text(ConsumidorNome) as ConsumidorNome,
    Text(ConsumidorNomeSocial) as ConsumidorNomeSocial,
    Text(ConsumidorSexo) as ConsumidorSexo,
    Text(ConsumidorEstadoCivil) as ConsumidorEstadoCivil,
    Date(ConsumidorDataNascimento) as ConsumidorDataNascimento,
    Text(ConsumidorCPF) as ConsumidorCPF,
    Text(ConsumidorNomeMae) as ConsumidorNomeMae,
    Text(ConsumidorBairro) as ConsumidorBairro,
    Text(ConsumidorMunicipio) as ConsumidorMunicipio,
    Text(ConsumidorUf) as ConsumidorUf
Resident ConsultaAtendimento
Where
    Not IsNull(__FK_consumidor);

Drop Table ConsultaAtendimento;
