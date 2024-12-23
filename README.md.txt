ff/process_models/README.md.txt        �  "json": {
            "almoxarifados": {
                "description": "Dep\u00f3sitos do SAP utilizados para armazenar items adquiridos de terceiros.",
                "identifier": "almoxarifados",
                "location": "",
                "name": "Almoxarifados",
                "schema": {}
            },
            "centros_de_custo": {
                "description": "",
                "identifier": "centros_de_custo",
                "location": "",
                "name": "Centros de Custo",
                "schema": {}
            },
            "culturas": {
                "description": "",
                "identifier": "culturas",
                "location": "",
                "name": "Culturas",
                "schema": {}
            },
            "departamentos": {
                "description": "",
                "identifier": "departamentos",
                "location": "",
                "name": "Departamentos",
                "schema": {}
            },
            "depositos": {
                "description": "",
                "identifier": "depositos",
                "location": "",
                "name": "Depositos",
                "schema": {}
            },
            "estados": {
                "description": "",
                "identifier": "estados",
                "location": "",
                "name": "Estados",
                "schema": {}
            },
            "filiais": {
                "description": "",
                "identifier": "filiais",
                "location": "",
                "name": "Filiais",
                "schema": {}
            },
            "natureza_da_declaracao": {
                "description": "",
                "identifier": "natureza_da_declaracao",
                "location": "",
                "name": "Natureza da Declaracao",
                "schema": {}
            },
            "safras": {
                "description": "",
                "identifier": "safras",
                "location": "",
                "name": "Safras",
                "schema": {}
            },
            "saplogin": {
                "description": "",
                "identifier": "saplogin",
                "location": "",
                "name": "SapLogin",
                "schema": {}
            },
            "tipo_conhecimento": {
                "description": "",
                "identifier": "tipo_conhecimento",
                "location": "",
                "name": "Tipo Conhecimento",
                "schema": {}
            },
            "tipo_declaracao": {
                "description": "",
                "identifier": "tipo_declaracao",
                "location": "",
                "name": "Tipo Declaracao",
                "schema": {}
            },
            "tipo_requisicao": {
                "description": "",
                "identifier": "tipo_requisicao",
                "location": "",
                "name": "Tipo Requisi\u00e7\u00e3o",
                "schema": {}
            },
            "utilizacoes": {
                "description": "",
                "identifier": "utilizacoes",
                "location": "",
                "name": "Utiliza\u00e7\u00f5es",
                "schema": {}
            }
        },
        "kkv": {
            "typeahead": {
                "description": "",
                "identifier": "typeahead",
                "location": "",
                "name": "Typeahead (modelo)",
                "schema": {}
            }
        }
    },
    "description": null,
    "display_name": ""
}:exclusiveGateway>
    <bpmn:sequenceFlow id="Flow_0e61uq9" sourceRef="Event_1f4ivqm" targetRef="Gateway_0n0ry39" />
    <bpmn:sequenceFlow id="Flow_1i8h7i6" sourceRef="Gateway_0n0ry39" targetRef="Activity_02tcc90" />
    <bpmn:sequenceFlow id="Flow_1m5c67s" sourceRef="Gateway_00db667" targetRef="Gateway_0n0ry39">
      <bpmn:conditionExpression>lancaNFeEntrada != 201</bpmn:conditionExpression>
    </bpmn:sequenceFlow>
    <bpmn:endEvent id="Event_1kdf3gn">
      <bpmn:incoming>Flow_1wb42r0</bpmn:incoming>
    </bpmn:endEvent>
    <bpmn:sequenceFlow id="Flow_1wb42r0" sourceRef="Gateway_00db667" targetRef="Event_1kdf3gn" />
    <bpmn:sequenceFlow id="Flow_02ido8m" sourceRef="Activity_02tcc90" targetRef="Gateway_01ugme4" />
    <bpmn:manualTask id="Activity_02tcc90" name="Verifica Erro na NFe">
      <bpmn:extensionElements>
        <spiffworkflow:preScript>try:
    status_code = lancaNFeEntrada 
    errorCode = rspEntrada['body']['error']['code']
    errorMessage = rspEntrada['body']['error']['message']['value']
except:
    command = errorEntrada['command_response_body']
    command = json.loads(command)
    status_code = errorEntrada['status_code']
    errorCode = errorEntrada['error_code']
    try:
        errorMessage = command['body']['error']['message']['value']
    except:
        errorMessage = command['body']['error']['message']</spiffworkflow:preScript>
        <spiffworkflow:instructionsForEndUser># &lt;font color="red"&gt;Esta operação resultou em erro&lt;/font&gt; :

### Informações

| Campo | Conteudo |
| ----------: | -------------- |
| Código Erro: | {{errorCode}} |
| Mensagem Erro: | {{errorMessage}}
| Status  | {{status_code}} |

1. Verifique se o erro é possível ser corrigido por você.
2. Qualquer outro erro, por favor entrar em contato com o TI.</spiffworkflow:instructionsForEndUser>
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_1i8h7i6</bpmn:incoming>
      <bpmn:outgoing>Flow_02ido8m</bpmn:outgoing>
    </bpmn:manualTask>
    <bpmn:boundaryEvent id="Event_02ztzva" attachedToRef="Activity_02tcc90">
      <bpmn:extensionElements>
        <spiffworkflow:signalButtonLabel>Encerrar</spiffworkflow:signalButtonLabel>
      </bpmn:extensionElements>
      <bpmn:outgoing>Flow_05o5om0</bpmn:outgoing>
      <bpmn:signalEventDefinition id="SignalEventDefinition_1jxvfn3" signalRef="Encerrar_Processo" />
    </bpmn:boundaryEvent>
    <bpmn:endEvent id="Event_1lgsabl">
      <bpmn:incoming>Flow_05o5om0</bpmn:incoming>
    </bpmn:endEvent>
    <bpmn:sequenceFlow id="Flow_05o5om0" sourceRef="Event_02ztzva" targetRef="Event_1lgsabl" />
  </bpmn:process>
  <bpmn:dataStore id="saplogin" name="JSONDataStore" />
  <bpmn:error id="Error_NFe_Entrada" name="Error_NFe_Entrada">
    <bpmn:extensionElements>
      <spiffworkflow:variableName>errorEntrada</spiffworkflow:variableName>
    </bpmn:extensionElements>
  </bpmn:error>
  <bpmn:signal id="Encerrar_Processo" name="Encerrar_Processo" />
  <bpmndi:BPMNDiagram id="BPMNDiagram_1">
    <bpmndi:BPMNPlane id="BPMNPlane_1" bpmnElement="Process_purchase_invoices_krrf890">
      <bpmndi:BPMNShape id="_BPMNShape_StartEvent_2" bpmnElement="StartEvent_1">
        <dc:Bounds x="179" y="159" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Gateway_01ugme4_di" bpmnElement="Gateway_01ugme4" isMarkerVisible="true">
        <dc:Bounds x="265" y="152" width="50" height="50" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Gateway_00db667_di" bpmnElement="Gateway_00db667" isMarkerVisible="true">
        <dc:Bounds x="595" y="152" width="50" height="50" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="DataStoreReference_13qzzrl_di" bpmnElement="DataStoreReference_13qzzrl">
        <dc:Bounds x="555" y="35" width="50" height="50" />
        <bpmndi:BPMNLabel>
          <dc:Bounds x="557" y="92" width="47" height="14" />
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1e3omg0_di" bpmnElement="Activity_1bq66l5">
        <dc:Bounds x="450" y="137" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Gateway_0n0ry39_di" bpmnElement="Gateway_0n0ry39" isMarkerVisible="true">
        <dc:Bounds x="495" y="285" width="50" height="50" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_1kdf3gn_di" bpmnElement="Event_1kdf3gn">
        <dc:Bounds x="692" y="159" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_0otkwr3_di" bpmnElement="Activity_02tcc90">
        <dc:Bounds x="330" y="270" width="100" height="80" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_1lgsabl_di" bpmnElement="Event_1lgsabl">
        <dc:Bounds x="472" y="412" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_0tu3t42_di" bpmnElement="Event_02ztzva">
        <dc:Bounds x="382" y="332" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_13ffjix_di" bpmnElement="Event_1f4ivqm">
        <dc:Bounds x="502" y="199" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNEdge id="Flow_0ijwrib_di" bpmnElement="Flow_0ijwrib">
        <di:waypoint x="215" y="177" />
        <di:waypoint x="265" y="177" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1r07qrf_di" bpmnElement="Flow_1r07qrf">
        <di:waypoint x="315" y="177" />
        <di:waypoint x="450" y="177" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_13gua63_di" bpmnElement="Flow_13gua63">
        <di:waypoint x="550" y="177" />
        <di:waypoint x="595" y="177" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="DataInputAssociation_0qgq4tq_di" bpmnElement="DataInputAssociation_0qgq4tq">
        <di:waypoint x="561" y="85" />
        <di:waypoint x="522" y="137" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0e61uq9_di" bpmnElement="Flow_0e61uq9">
        <di:waypoint x="520" y="235" />
        <di:waypoint x="520" y="285" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1i8h7i6_di" bpmnElement="Flow_1i8h7i6">
        <di:waypoint x="495" y="310" />
        <di:waypoint x="430" y="310" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1m5c67s_di" bpmnElement="Flow_1m5c67s">
        <di:waypoint x="620" y="202" />
        <di:waypoint x="620" y="310" />
        <di:waypoint x="545" y="310" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1wb42r0_di" bpmnElement="Flow_1wb42r0">
        <di:waypoint x="645" y="177" />
        <di:waypoint x="692" y="177" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_02ido8m_di" bpmnElement="Flow_02ido8m">
        <di:waypoint x="330" y="310" />
        <di:waypoint x="290" y="310" />
        <di:waypoint x="290" y="202" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_05o5om0_di" bpmnElement="Flow_05o5om0">
        <di:waypoint x="400" y="368" />
        <di:waypoint x="400" y="430" />
        <di:waypoint x="472" y="430" />
      </bpmndi:BPMNEdge>
    </bpmndi:BPMNPlane>
  </bpmndi:BPMNDiagram>
</bpmn:definitions>
  <bpmn:exclusiveGateway id="Gateway_0osfbsk">
      <bpmn:incoming>Flow_1dd3rlu</bpmn:incoming>
      <bpmn:incoming>Flow_0wl0noj</bpmn:incoming>
      <bpmn:outgoing>Flow_1x9gvlk</bpmn:outgoing>
    </bpmn:exclusiveGateway>
    <bpmn:sequenceFlow id="Flow_1x9gvlk" sourceRef="Gateway_0osfbsk" targetRef="Activity_1d81loa" />
    <bpmn:sequenceFlow id="Flow_0wl0noj" sourceRef="Gateway_1tmpqad" targetRef="Gateway_0osfbsk">
      <bpmn:conditionExpression>lancado != 204</bpmn:conditionExpression>
    </bpmn:sequenceFlow>
    <bpmn:exclusiveGateway id="Gateway_1ent8h0" default="Flow_1uor4aj">
      <bpmn:incoming>Flow_0htr4uy</bpmn:incoming>
      <bpmn:outgoing>Flow_1uor4aj</bpmn:outgoing>
      <bpmn:outgoing>Flow_0v9pdgb</bpmn:outgoing>
    </bpmn:exclusiveGateway>
    <bpmn:sequenceFlow id="Flow_1uor4aj" sourceRef="Gateway_1ent8h0" targetRef="Gateway_0069475" />
    <bpmn:endEvent id="Event_1j6jhp3">
      <bpmn:incoming>Flow_0v9pdgb</bpmn:incoming>
    </bpmn:endEvent>
    <bpmn:sequenceFlow id="Flow_0v9pdgb" sourceRef="Gateway_1ent8h0" targetRef="Event_1j6jhp3">
      <bpmn:conditionExpression>lancado != 201</bpmn:conditionExpression>
    </bpmn:sequenceFlow>
    <bpmn:dataStoreReference id="DataStoreReference_1ql4o3n" name="SapLogin" dataStoreRef="saplogin" type="json" />
    <bpmn:boundaryEvent id="Event_1aqlqgv" attachedToRef="Activity_1206m73">
      <bpmn:outgoing>Flow_1noa3xy</bpmn:outgoing>
      <bpmn:errorEventDefinition id="ErrorEventDefinition_05s076g" errorRef="ErrorInutilizarNFe" />
    </bpmn:boundaryEvent>
    <bpmn:sequenceFlow id="Flow_1noa3xy" sourceRef="Event_1aqlqgv" targetRef="Gateway_1tmpqad" />
    <bpmn:sequenceFlow id="Flow_0y3xh1b" sourceRef="Event_04w731w" targetRef="Activity_0yjpt9c" />
    <bpmn:endEvent id="Event_0d5o65q">
      <bpmn:incoming>Flow_1tm2dat</bpmn:incoming>
    </bpmn:endEvent>
    <bpmn:sequenceFlow id="Flow_1tm2dat" sourceRef="Activity_0yjpt9c" targetRef="Event_0d5o65q" />
    <bpmn:scriptTask id="Activity_0yjpt9c" name="Gera Lancado">
      <bpmn:incoming>Flow_0y3xh1b</bpmn:incoming>
      <bpmn:outgoing>Flow_1tm2dat</bpmn:outgoing>
      <bpmn:script>lancado = ErrorNFe['status_code']</bpmn:script>
    </bpmn:scriptTask>
  </bpmn:process>
  <bpmn:dataStore id="saplogin" name="JSONDataStore" />
  <bpmn:signal id="inutiliza" name="inutiliza" />
  <bpmn:error id="ErrorEmiteNFe" name="ErrorEmiteNFe">
    <bpmn:extensionElements>
      <spiffworkflow:variableName>ErrorNFe</spiffworkflow:variableName>
    </bpmn:extensionElements>
  </bpmn:error>
  <bpmn:error id="ErrorInutilizarNFe" name="ErrorInutilizarNFe">
    <bpmn:extensionElements>
      <spiffworkflow:variableName>ErrorInutiliza</spiffworkflow:variableName>
    </bpmn:extensionElements>
  </bpmn:error>
  <bpmndi:BPMNDiagram id="BPMNDiagram_1">
    <bpmndi:BPMNPlane id="BPMNPlane_1" bpmnElement="Process_invoices_post_xf8j10r">
      <bpmndi:BPMNShape id="_BPMNShape_StartEvent_2" bpmnElement="StartEvent_1">
        <dc:Bounds x="179" y="159" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_15mqiq1_di" bpmnElement="Activity_0slsnk1">
        <dc:Bounds x="310" y="137" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="DataStoreReference_1w94a7o_di" bpmnElement="DataStoreReference_1w94a7o">
        <dc:Bounds x="235" y="255" width="50" height="50" />
        <bpmndi:BPMNLabel>
          <dc:Bounds x="237" y="312" width="47" height="14" />
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Gateway_0069475_di" bpmnElement="Gateway_0069475" isMarkerVisible="true">
        <dc:Bounds x="655" y="152" width="50" height="50" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_1w5t3go_di" bpmnElement="Event_07f7330">
        <dc:Bounds x="802" y="159" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1fvvdiz_di" bpmnElement="Activity_1oobqq4">
        <dc:Bounds x="950" y="137" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Gateway_1rq0zkg_di" bpmnElement="Gateway_1rq0zkg" isMarkerVisible="true">
        <dc:Bounds x="1145" y="152" width="50" height="50" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_1i4rvuz_di" bpmnElement="Event_1i4rvuz">
        <dc:Bounds x="1302" y="159" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1aihu5n_di" bpmnElement="Activity_1d81loa">
        <dc:Bounds x="940" y="290" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_0q9rl2x_di" bpmnElement="Activity_1206m73">
        <dc:Bounds x="940" y="460" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Gateway_1tmpqad_di" bpmnElement="Gateway_1tmpqad" isMarkerVisible="true">
        <dc:Bounds x="1145" y="475" width="50" height="50" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_17668b0_di" bpmnElement="Event_17668b0">
        <dc:Bounds x="1302" y="482" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Gateway_0osfbsk_di" bpmnElement="Gateway_0osfbsk" isMarkerVisible="true">
        <dc:Bounds x="1145" y="305" width="50" height="50" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Gateway_1ent8h0_di" bpmnElement="Gateway_1ent8h0" isMarkerVisible="true">
        <dc:Bounds x="505" y="152" width="50" height="50" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_1j6jhp3_di" bpmnElement="Event_1j6jhp3">
        <dc:Bounds x="602" y="312" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="DataStoreReference_1ql4o3n_di" bpmnElement="DataStoreReference_1ql4o3n">
        <dc:Bounds x="825" y="555" width="50" height="50" />
        <bpmndi:BPMNLabel>
          <dc:Bounds x="827" y="612" width="47" height="14" />
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_0d5o65q_di" bpmnElement="Event_0d5o65q">
        <dc:Bounds x="602" y="402" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1t1aj0p_di" bpmnElement="Activity_0yjpt9c">
        <dc:Bounds x="450" y="380" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_0rwxwr3_di" bpmnElement="Event_1aqlqgv">
        <dc:Bounds x="972" y="522" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_08akdo1_di" bpmnElement="Event_153wc1q">
        <dc:Bounds x="972" y="352" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_1n66gzz_di" bpmnElement="Event_04w731w">
        <dc:Bounds x="362" y="199" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNEdge id="Flow_1enkyef_di" bpmnElement="Flow_1enkyef">
        <di:waypoint x="215" y="177" />
        <di:waypoint x="310" y="177" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="DataInputAssociation_1se6ii5_di" bpmnElement="DataInputAssociation_1se6ii5">
        <di:waypoint x="285" y="260" />
        <di:waypoint x="339" y="217" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0htr4uy_di" bpmnElement="Flow_0htr4uy">
        <di:waypoint x="410" y="177" />
        <di:waypoint x="505" y="177" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0bpq1s0_di" bpmnElement="Flow_0bpq1s0">
        <di:waypoint x="705" y="177" />
        <di:waypoint x="802" y="177" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0r122ep_di" bpmnElement="Flow_0r122ep">
        <di:waypoint x="838" y="177" />
        <di:waypoint x="950" y="177" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0vn1oa8_di" bpmnElement="Flow_0vn1oa8">
        <di:waypoint x="1050" y="177" />
        <di:waypoint x="1145" y="177" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1o36j2p_di" bpmnElement="Flow_1o36j2p">
        <di:waypoint x="1195" y="177" />
        <di:waypoint x="1302" y="177" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1dd3rlu_di" bpmnElement="Flow_1dd3rlu">
        <di:waypoint x="1170" y="202" />
        <di:waypoint x="1170" y="305" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1pbq4ko_di" bpmnElement="Flow_1pbq4ko">
        <di:waypoint x="940" y="330" />
        <di:waypoint x="680" y="330" />
        <di:waypoint x="680" y="202" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_09t17f7_di" bpmnElement="Flow_09t17f7">
        <di:waypoint x="990" y="388" />
        <di:waypoint x="990" y="460" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="DataInputAssociation_0n9rl9q_di" bpmnElement="DataInputAssociation_0n9rl9q">
        <di:waypoint x="875" y="571" />
        <di:waypoint x="962" y="540" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0wz143b_di" bpmnElement="Flow_0wz143b">
        <di:waypoint x="1040" y="500" />
        <di:waypoint x="1145" y="500" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_06qx27n_di" bpmnElement="Flow_06qx27n">
        <di:waypoint x="1195" y="500" />
        <di:waypoint x="1302" y="500" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1x9gvlk_di" bpmnElement="Flow_1x9gvlk">
        <di:waypoint x="1145" y="330" />
        <di:waypoint x="1040" y="330" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0wl0noj_di" bpmnElement="Flow_0wl0noj">
        <di:waypoint x="1170" y="475" />
        <di:waypoint x="1170" y="355" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1uor4aj_di" bpmnElement="Flow_1uor4aj">
        <di:waypoint x="555" y="177" />
        <di:waypoint x="655" y="177" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0v9pdgb_di" bpmnElement="Flow_0v9pdgb">
        <di:waypoint x="530" y="202" />
        <di:waypoint x="530" y="330" />
        <di:waypoint x="602" y="330" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1noa3xy_di" bpmnElement="Flow_1noa3xy">
        <di:waypoint x="990" y="558" />
        <di:waypoint x="990" y="610" />
        <di:waypoint x="1170" y="610" />
        <di:waypoint x="1170" y="525" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0y3xh1b_di" bpmnElement="Flow_0y3xh1b">
        <di:waypoint x="380" y="235" />
        <di:waypoint x="380" y="420" />
        <di:waypoint x="450" y="420" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1tm2dat_di" bpmnElement="Flow_1tm2dat">
        <di:waypoint x="550" y="420" />
        <di:waypoint x="602" y="420" />
      </bpmndi:BPMNEdge>
    </bpmndi:BPMNPlane>
  </bpmndi:BPMNDiagram>
</bpmn:definitions>
Elements>
      <bpmn:incoming>Flow_1g6680p</bpmn:incoming>
      <bpmn:incoming>Flow_1ymf5ls</bpmn:incoming>
      <bpmn:outgoing>Flow_1yy09pu</bpmn:outgoing>
    </bpmn:userTask>
    <bpmn:dataStoreReference id="DataStoreReference_044vwcr" name="Culturas" dataStoreRef="culturas" type="json" />
    <bpmn:dataStoreReference id="DataStoreReference_14r9weh" name="Safras" dataStoreRef="safras" type="json" />
    <bpmn:dataStoreReference id="DataStoreReference_0yj9799" name="Filiais" dataStoreRef="filiais" type="json" />
    <bpmn:exclusiveGateway id="Gateway_1nqm8kc" default="Flow_18vwk2i">
      <bpmn:incoming>Flow_1yy09pu</bpmn:incoming>
      <bpmn:outgoing>Flow_18vwk2i</bpmn:outgoing>
      <bpmn:outgoing>Flow_1q3qvan</bpmn:outgoing>
    </bpmn:exclusiveGateway>
    <bpmn:exclusiveGateway id="Gateway_1cfqyfk" default="Flow_041vp20">
      <bpmn:incoming>Flow_1gun2i8</bpmn:incoming>
      <bpmn:outgoing>Flow_041vp20</bpmn:outgoing>
      <bpmn:outgoing>Flow_1dwzd8i</bpmn:outgoing>
    </bpmn:exclusiveGateway>
    <bpmn:task id="Activity_0ck9cww" name="Verifica erro">
      <bpmn:incoming>Flow_0lkxegk</bpmn:incoming>
      <bpmn:outgoing>Flow_10hhtnr</bpmn:outgoing>
    </bpmn:task>
    <bpmn:dataStoreReference id="DataStoreReference_1175xbr" name="SapLogin" dataStoreRef="saplogin" type="json" />
    <bpmn:manualTask id="Activity_1ly0k48" name="Verifica Erro">
      <bpmn:extensionElements>
        <spiffworkflow:preScript>try:
    status_code = lancado
    errorCode = rsp['body']['error']['code']
    errorMessage = rsp['body']['error']['message']['value']
except:
    status_code = sapError['status_code']
    errorCode = sapError['error_code']
    errorMessage = sapError['message']</spiffworkflow:preScript>
        <spiffworkflow:instructionsForEndUser># &lt;font color="red"&gt;Esta operação resultou em erro&lt;/font&gt; :

### Informações

| Campo | Conteudo |
| ----------: | -------------- |
| Código Erro: | {{errorCode}} |
| Mensagem Erro: | {{errorMessage}}
| Status  | {{status_code}} |

1. Verifique se o erro é possível ser corrigido por você, por exemplo: "Quantidade decai para estoque negativo". O item que você está tentando faturar **não tem estoque no SAP.**
2. Qualquer outro erro, por favor entrar em contato com o TI.</spiffworkflow:instructionsForEndUser>
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_0x5wk77</bpmn:incoming>
      <bpmn:incoming>Flow_1dwzd8i</bpmn:incoming>
      <bpmn:outgoing>Flow_1ymf5ls</bpmn:outgoing>
    </bpmn:manualTask>
    <bpmn:boundaryEvent id="Event_06i6v6d" attachedToRef="Activity_0nynyx4">
      <bpmn:outgoing>Flow_0x5wk77</bpmn:outgoing>
      <bpmn:errorEventDefinition id="ErrorEventDefinition_0pr9ad2" errorRef="ErrorSap" />
    </bpmn:boundaryEvent>
    <bpmn:boundaryEvent id="Event_1luisbh" attachedToRef="Activity_00vuw5a">
      <bpmn:outgoing>Flow_0lkxegk</bpmn:outgoing>
      <bpmn:errorEventDefinition id="ErrorEventDefinition_008y1vx" errorRef="ErrorDePara" />
    </bpmn:boundaryEvent>
    <bpmn:sequenceFlow id="Flow_17db3yp" sourceRef="StartEvent_1" targetRef="Activity_0qpzdpu" />
    <bpmn:sequenceFlow id="Flow_1tvkyw7" sourceRef="Activity_1gq0mev" targetRef="Activity_00vuw5a" />
    <bpmn:sequenceFlow id="Flow_06zd818" sourceRef="Activity_00vuw5a" targetRef="Activity_1x5vkae" />
    <bpmn:sequenceFlow id="Flow_0bvco56" sourceRef="Gateway_1fdiwv1" targetRef="Activity_0qpzdpu">
      <bpmn:conditionExpression>operacao == 'Corrige'</bpmn:conditionExpression>
    </bpmn:sequenceFlow>
    <bpmn:sequenceFlow id="Flow_1q3qvan" sourceRef="Gateway_1nqm8kc" targetRef="Activity_0qpzdpu">
      <bpmn:conditionExpression>operacao == 'Corrige'</bpmn:conditionExpression>
    </bpmn:sequenceFlow>
    <bpmn:sequenceFlow id="Flow_10hhtnr" sourceRef="Activity_0ck9cww" targetRef="Activity_0qpzdpu" />
    <bpmn:sequenceFlow id="Flow_081crpr" sourceRef="Activity_0qpzdpu" targetRef="Activity_1gq0mev" />
    <bpmn:sequenceFlow id="Flow_1ejzlor" sourceRef="Activity_1nr33uk" targetRef="Event_0x3itur" />
    <bpmn:sequenceFlow id="Flow_0kvuaau" sourceRef="Activity_0pk9g8b" targetRef="Activity_1nr33uk" />
    <bpmn:sequenceFlow id="Flow_041vp20" sourceRef="Gateway_1cfqyfk" targetRef="Activity_0pk9g8b" />
    <bpmn:sequenceFlow id="Flow_0plksld" sourceRef="Activity_1x5vkae" targetRef="Gateway_1fdiwv1" />
    <bpmn:sequenceFlow id="Flow_1g6680p" sourceRef="Gateway_1fdiwv1" targetRef="Activity_0w2moib" />
    <bpmn:sequenceFlow id="Flow_18vwk2i" sourceRef="Gateway_1nqm8kc" targetRef="Activity_0nynyx4" />
    <bpmn:sequenceFlow id="Flow_1gun2i8" sourceRef="Activity_0nynyx4" targetRef="Gateway_1cfqyfk" />
    <bpmn:sequenceFlow id="Flow_1ymf5ls" sourceRef="Activity_1ly0k48" targetRef="Activity_0w2moib" />
    <bpmn:sequenceFlow id="Flow_1yy09pu" sourceRef="Activity_0w2moib" targetRef="Gateway_1nqm8kc" />
    <bpmn:sequenceFlow id="Flow_1dwzd8i" sourceRef="Gateway_1cfqyfk" targetRef="Activity_1ly0k48">
      <bpmn:conditionExpression>lancado != 201</bpmn:conditionExpression>
    </bpmn:sequenceFlow>
    <bpmn:sequenceFlow id="Flow_0lkxegk" sourceRef="Event_1luisbh" targetRef="Activity_0ck9cww" />
    <bpmn:sequenceFlow id="Flow_0x5wk77" sourceRef="Event_06i6v6d" targetRef="Activity_1ly0k48" />
  </bpmn:process>
  <bpmn:error id="ErrorSap" name="ErrorSap">
    <bpmn:extensionElements>
      <spiffworkflow:variableName>sapError</spiffworkflow:variableName>
    </bpmn:extensionElements>
  </bpmn:error>
  <bpmn:error id="ErrorDePara" name="ErrorDePara">
    <bpmn:extensionElements>
      <spiffworkflow:variableName>DeParaError</spiffworkflow:variableName>
    </bpmn:extensionElements>
  </bpmn:error>
  <bpmndi:BPMNDiagram id="BPMNDiagram_1">
    <bpmndi:BPMNPlane id="BPMNPlane_1" bpmnElement="Collaboration_1nlwobl">
      <bpmndi:BPMNShape id="Participant_0x0t826_di" bpmnElement="Participant_0x0t826" isHorizontal="true">
        <dc:Bounds x="815" y="301" width="2399" height="1044" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Lane_0ggjzat_di" bpmnElement="Lane_contabil" isHorizontal="true">
        <dc:Bounds x="845" y="1015" width="2369" height="330" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Lane_1aovmuh_di" bpmnElement="Lane" isHorizontal="true">
        <dc:Bounds x="845" y="604" width="2369" height="411" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Lane_0c5w8vb_di" bpmnElement="Lane_rh" isHorizontal="true">
        <dc:Bounds x="845" y="301" width="2369" height="303" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="_BPMNShape_StartEvent_2" bpmnElement="StartEvent_1">
        <dc:Bounds x="865" y="344" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_00vuw5a_di" bpmnElement="Activity_00vuw5a" isExpanded="true">
        <dc:Bounds x="916" y="665" width="920" height="200" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_17u4mx7_di" bpmnElement="Event_17u4mx7">
        <dc:Bounds x="966" y="747" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_00k0sz6_di" bpmnElement="Activity_0yrlrcw">
        <dc:Bounds x="1056" y="725" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1llcud8_di" bpmnElement="Activity_0tb9ude">
        <dc:Bounds x="1216" y="725" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1h639oh_di" bpmnElement="Activity_1hjm5ca">
        <dc:Bounds x="1376" y="725" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_0m9p92l_di" bpmnElement="Activity_1bvnfh7">
        <dc:Bounds x="1536" y="725" width="100" height="80" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_170pr7f_di" bpmnElement="Event_170pr7f">
        <dc:Bounds x="1698" y="747" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNEdge id="Flow_0vz4nph_di" bpmnElement="Flow_0vz4nph">
        <di:waypoint x="1002" y="765" />
        <di:waypoint x="1056" y="765" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0hyo4rk_di" bpmnElement="Flow_0hyo4rk">
        <di:waypoint x="1156" y="765" />
        <di:waypoint x="1216" y="765" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0p880da_di" bpmnElement="Flow_0p880da">
        <di:waypoint x="1316" y="765" />
        <di:waypoint x="1376" y="765" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0gjw4os_di" bpmnElement="Flow_0gjw4os">
        <di:waypoint x="1476" y="765" />
        <di:waypoint x="1536" y="765" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0de8f5g_di" bpmnElement="Flow_0de8f5g">
        <di:waypoint x="1636" y="765" />
        <di:waypoint x="1698" y="765" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNShape id="Activity_0sl2fzs_di" bpmnElement="Activity_0qpzdpu">
        <dc:Bounds x="966" y="322" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1fn7pr1_di" bpmnElement="Activity_1gq0mev">
        <dc:Bounds x="1126" y="322" width="100" height="80" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_0x3itur_di" bpmnElement="Event_0x3itur">
        <dc:Bounds x="3118" y="344" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1tzg16p_di" bpmnElement="Activity_1nr33uk">
        <dc:Bounds x="2976" y="322" width="100" height="80" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_0azzpb8_di" bpmnElement="Activity_0pk9g8b">
        <dc:Bounds x="2816" y="1085" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1gy6ua9_di" bpmnElement="Activity_1x5vkae">
        <dc:Bounds x="1886" y="322" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Gateway_1fdiwv1_di" bpmnElement="Gateway_1fdiwv1" isMarkerVisible="true">
        <dc:Bounds x="2041" y="337" width="50" height="50" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1g5hxev_di" bpmnElement="Activity_0nynyx4">
        <dc:Bounds x="2516" y="1085" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1v3eutn_di" bpmnElement="Activity_0w2moib">
        <dc:Bounds x="2176" y="1085" width="100" height="80" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="DataStoreReference_044vwcr_di" bpmnElement="DataStoreReference_044vwcr">
        <dc:Bounds x="1071" y="530" width="50" height="50" />
        <bpmndi:BPMNLabel>
          <dc:Bounds x="1075" y="587" width="42" height="14" />
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="DataStoreReference_14r9weh_di" bpmnElement="DataStoreReference_14r9weh">
        <dc:Bounds x="1021" y="530" width="50" height="50" />
        <bpmndi:BPMNLabel>
          <dc:Bounds x="1029" y="587" width="35" height="14" />
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNShape>
   