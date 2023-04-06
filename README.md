# AMMO Ontology

The Additive Manufacturing Maintenance Ontology (AMMO) is an ontology designed to support the maintenance of US Air Force equipment using additive manufacturing techniques. The ontology is being developed to facilitate the creation of replacement parts through additive manufacturing, and to ensure that these parts meet the required specifications and safety standards.

## Ontology Structure

The AMMO ontology consists of several modules, each with a specific focus:

- Equipment: Provides information on the equipment used to manufacture replacement parts.
- Materials: Provides information on the materials used to manufacture replacement parts.
- Processes: Provides information on the 3D printing processes used to manufacture replacement parts.
- Maintenance Tasks: Provides information on the maintenance tasks performed on the equipment used to manufacture replacement parts.
- Failure Modes and Effects: Provides information on the potential failure modes and effects of replacement parts.
- Quality Control and Inspection: Provides information on the quality control and inspection procedures used to ensure the manufactured parts meet the required specifications.
- Human Roles: Provides information on the roles of the personnel involved in the additive manufacturing process.
- Regulations and Standards: Provides information on the regulations and standards that must be met for replacement parts to be considered safe and compliant.
- Safety and Environmental Considerations: Provides information on the safety and environmental considerations for replacement parts.

Each module is defined in a separate Turtle file, located in the `modules/` directory.

## Ontology Versions

The AMMO ontology is versioned using [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html). Each version is stored in the `versions/` directory, and includes the concatenated ontology in several formats (Turtle, RDF/XML, and JSON-LD).

## Documentation

The AMMO ontology documentation is generated from the Turtle file using [PyLODE](https://github.com/essepuntato/PyLODE). The HTML documentation can be found in the `documentation/` directory.

## Usage

To use the AMMO ontology in your project, import the latest version of the ontology using the following URI:

```
https://w3id.org/ammo/ont/latest
```


If you require a specific version of the ontology, you can use the following URI pattern:

```
https://w3id.org/ammo/ont/<version>
```



Replace `<version>` with the version number you require.

## Contributing

To contribute to the AMMO ontology, please submit a pull request to the `develop` branch of the [AMMO repository](https://github.com/your-username/ammo-ontology). 

## License

The AMMO ontology is licensed under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).


## Purpose
The Additive Manufacturing Maintenance Ontology (AMMO) is an ontology developed to support the maintenance operations of the US Air Force in the context of additive manufacturing. AMMO is designed to provide a semantic framework for capturing and representing information related to the replacement of parts using additive manufacturing processes. The ontology is intended to serve as a knowledge base for an LLM (Language and Learning Model) assistant, which can guide maintenance personnel in the selection of the appropriate additive manufacturing processes and materials for producing replacement parts.

AMMO is developed with the goal of improving the efficiency and effectiveness of maintenance operations through the use of semantic technologies. The ontology is designed to be integrated with existing systems, such as LangChain and LLMAindex, to provide a comprehensive approach to maintenance operations in the US Air Force. By leveraging JSON-LD and semantic APIs, AMMO can be easily integrated into other software systems and can enable data interoperability between different systems.

Overall, AMMO is developed to provide a semantic framework for capturing and representing information related to additive manufacturing and maintenance operations, with the goal of improving the efficiency and effectiveness of maintenance operations in the US Air Force.

### Large Language Models
Recent advances in Natural Language Processing (NLP) have led to the development of Large Language Models (LLMs), such as GPT-3, which have demonstrated remarkable performance in a variety of tasks, including language understanding, generation, and translation. However, as these models become more prevalent, it is increasingly important to ensure that their outputs are aligned with specific domains and contexts. Ontologies, such as the AMMO ontology, play a crucial role in providing a structured and formal representation of knowledge in a particular domain, enabling LLMs to better understand the context and produce more accurate and relevant outputs. By incorporating the AMMO ontology into the training and deployment of LLMs, we can improve the quality and accuracy of language models, making them more useful in practical applications such as the LangChain and LLMAindex projects.

## Competency Questions
Competency questions are a set of high-level questions that an ontology is expected to answer. These questions help to ensure that the ontology is fit for purpose and provides the necessary information to meet the needs of its intended users. Here are some example competency questions for the AMMO ontology:

1. What equipment is required to manufacture a replacement part for a given system?

```json
{
  "@context": {
    "@version": 1.1,
    "id": "@id",
    "type": "@type",
    "version": "http://purl.org/pav/version",
    "question": "http://www.w3.org/2004/02/skos/core#definition",
    "query": "http://www.w3.org/2004/02/skos/core#notation",
    "expected_output": {
      "@container": "@list",
      "@id": "http://schema.org/ItemList"
    }
  },
  "id": "1",
  "type": "CompetencyQuestion",
  "version": "2.0",
  "question": "What equipment is required to manufacture a replacement part for a given system?",
  "query": "PREFIX ammo: <https://w3id.org/ammo/ont/> SELECT DISTINCT ?equipment WHERE { ?equipment a ammo:Equipment ; ammo:isRequiredForManufacturing ammo:System }",
  "expected_output": [
    "https://w3id.org/ammo/ont#3DPrinter",
    "https://w3id.org/ammo/ont#PowderBedFusionSystem",
    "https://w3id.org/ammo/ont#BinderJettingSystem"
  ]
}
```

2. What are the potential failure modes and effects of a replacement part for a given system?

```json
{
    "@context": {
      "@version": 1.1,
      "id": "@id",
      "type": "@type",
      "version": "http://purl.org/pav/version",
      "question": "http://www.w3.org/2004/02/skos/core#definition",
      "query": "http://www.w3.org/2004/02/skos/core#notation",
      "expected_output": {
        "@container": "@list",
        "@id": "http://schema.org/ItemList"
      }
    },
    "id": "7",
    "type": "CompetencyQuestion",
    "version": "1.0.0",
    "question": "What are the potential failure modes and effects of a replacement part for a given system?",
    "query": "PREFIX ammo: <https://w3id.org/ammo/ont/>\
              PREFIX qudt: <http://qudt.org/schema/qudt/>\
              SELECT ?part ?failure_mode ?effect WHERE {\
                ?part a ammo:ReplacementPart;\
                ammo:hasFailureMode ?failure_mode.\
                ?failure_mode ammo:hasEffect ?effect.\
                ?failure_mode ammo:hasSeverity ?severity.\
                ?severity qudt:unit ?unit.\
                ?severity qudt:numericValue ?value.\
                FILTER(?value >= 0.7)\
              }",
    "expected_output": [      {        "@type": "ReplacementPart",        "name": "Part1",        "hasFailureMode": [          {            "@type": "FailureMode",            "name": "FailureMode1",            "hasEffect": [              {                "@type": "Effect",                "name": "Effect1"              }            ],
            "hasSeverity": [              {                "@type": "Severity",                "name": "Severity1",                "numericValue": "0.8",                "unit": "http://qudt.org/vocab/unit#Percent"              }            ]
          },
          {
            "@type": "FailureMode",
            "name": "FailureMode2",
            "hasEffect": [
              {
                "@type": "Effect",
                "name": "Effect2"
              }
            ],
            "hasSeverity": [
              {
                "@type": "Severity",
                "name": "Severity2",
                "numericValue": "0.9",
                "unit": "http://qudt.org/vocab/unit#Percent"
              }
            ]
          }
        ]
      }
    ]
  }
```


## ChatGPT as Modeling Assistant
This ontology was developed with the help of ChatGPT, a large language model developed by OpenAI based on the GPT-3.5 architecture. ChatGPT was able to provide suggestions and guidance on the ontology development process, such as identifying potential modules and helping to refine the competency questions.

ChatGPT was particularly useful in providing background knowledge and helping to identify potential issues and considerations in the ontology development process. Its ability to understand and generate natural language allowed for a more intuitive and streamlined workflow in developing the ontology.

### ChatGPT Logs
The logs of the chat sessions with ChatGPT during the ontology development process are available in the chatgpt_logs directory. These logs provide a detailed record of the interactions with ChatGPT, including the questions asked and the responses generated by the model. The logs can be used for reference and to provide transparency into the ontology development process.

## ChatGPT Prompts

### ChatGPT Prompt: Equipment Module

Hi ChatGPT! I'm working on the Additive Manufacturing Ontology (AMMO) project, which aims to provide a standardized way of representing knowledge related to additive manufacturing processes. Our ontology is available in a GitHub repository at https://github.com/your-username/ammo.

Our ontology is structured using a modular approach, with separate turtle files for each module, and a script that concatenates them all together. We've already created the common_metadata.ttl module, which contains metadata about the ontology, and the equipment_module.ttl module, which contains information about the equipment used to manufacture replacement parts.

We'd like to further develop the equipment module to include more detailed information about the equipment, such as manufacturer, model, and capabilities. Our goal is to provide enough information to determine whether a particular piece of equipment is suitable for producing a replacement part for a given system.

Could you help us generate some more detailed classes and properties for the equipment module, using the URI https://w3id.org/ammo/ont/ and the prefix ammo:? We've already created a stub for the module, which you can find in the modules/equipment_module.ttl file of our GitHub repository.

Once we've completed the module, we'll use the concatenate_ontology.py script in the repository to merge the module into the full AMMO ontology. We'd also like to use ChatGPT to help us generate documentation for the ontology, using the generate_documentation.py script.

Thanks for your help!

### ChatGPT Prompt: Materials Module

Hello ChatGPT! I'm starting a new session to model the Materials module of the AMMO ontology. 

As a reminder, the ontology prefix is "ammo" and the URI is <https://w3id.org/ammo/ont/>. The ontology has a modular structure consisting of separate turtle files for each module, as well as a common_metadata.ttl module. The modules are: Equipment, Materials, Processes, Maintenance Tasks, Failure Modes and Effects, Quality Control and Inspection, Human Roles, Regulations and Standards, and Safety and Environmental Considerations.

The equipment module has already been modeled and can be found in the "equipment_module.ttl" file in the "modules" directory. The metadata for the ontology can be found in the "common_metadata.ttl" module. All modules should import the common_metadata.ttl module. 

For this session, I would like to focus on the Materials module. The purpose of this module is to provide information on the materials that will be used to manufacture replacement parts, including their composition, properties, and behavior during the additive manufacturing process.

To get started, can you help me define the classes and properties needed for this module? Please keep in mind the domain and range of each property, as well as any existing vocabularies we can reuse. Let's create a separate turtle file for this module called "materials_module.ttl" in the "modules" directory.

When you are done, please save the resulting turtle file and update the concatenate_ontology.py script to include it when generating the full AMMO ontology. You can also update the documentation by running the generate_documentation.py script.

Thank you for your help!

### ChatGPT Prompt: Process Module

Hi ChatGPT, I'd like to continue modeling the AMMO ontology, specifically the Processes module. 

Just as a reminder, the purpose of this module is to provide information on the 3D printing processes that will be used to manufacture replacement parts. 

The ontology prefix is "ammo" and the URI is <https://w3id.org/ammo/ont/>. 

We've already created the module stub file "processes_module.ttl" with the appropriate prefix and ontology information. Here are the classes and properties we'll need to define:

Classes:
- ammo:Process
- ammo:3DPrintingProcess

Properties:
- ammo:hasProcessType
- ammo:hasProcessDescription
- ammo:hasProcessMaterial
- ammo:hasProcessParameter

Please provide me with the definitions for these classes and properties.

### ChatGPT Prompt: Maintenanece Tasks

Modeling the Maintenance Tasks Module of the AMMO ontology.

The Maintenance Tasks module provides information on the maintenance tasks that will be performed on the equipment used to manufacture replacement parts through additive manufacturing.

The module should include information on the types of maintenance tasks, frequency of maintenance, recommended maintenance procedures, and personnel responsible for performing the tasks.

The AMMO ontology is structured into several modules, each providing information on a specific aspect of the additive manufacturing process. The modules are:
- Equipment
- Materials
- Processes
- Maintenance Tasks
- Failure Modes and Effects
- Quality Control and Inspection
- Human Roles
- Regulations and Standards
- Safety and Environmental Considerations

The ontology is available on GitHub at https://github.com/example/ammo-ontology and follows a modular structure. The maintenance tasks module should be added to the appropriate turtle file in the modules directory.

The ontology URI is <https://w3id.org/ammo/ont/> and the prefix is "ammo". The ontology follows the FAIR principles and metadata is provided in the common_metadata.ttl module.

To model the Maintenance Tasks module, consider the following questions:
- What are the types of maintenance tasks that need to be performed on the equipment?
- How frequently should maintenance be performed?
- What are the recommended maintenance procedures?
- Who is responsible for performing the maintenance tasks?

Please use the existing equipment module as a reference for how to structure the Maintenance Tasks module. Use the prefix "ammo-mt" for any new classes, properties, or individuals created in the module. Don't forget to update the common_metadata.ttl module with any new ontology metadata.

### ChatGPT Prompt: Failure Modes and Effects Module
I am starting a new ChatGPT session to model the Failure Modes and Effects module for the AMMO ontology. The ontology consists of several modules, including Equipment, Materials, Processes, Maintenance Tasks, Quality Control and Inspection, Human Roles, Regulations and Standards, and Safety and Environmental Considerations. The goal of this session is to model the Failure Modes and Effects module, which can provide information on the potential failure modes and effects of the replacement parts manufactured using additive manufacturing technology.

The Equipment module provides information on the equipment used to manufacture the replacement parts, including the manufacturer, model number, and specifications.

The Materials module provides information on the materials used to manufacture the replacement parts, including the material type, properties, and performance characteristics.

The Processes module provides information on the 3D printing processes used to manufacture the replacement parts, including the type of process, parameters, and settings.

The Maintenance Tasks module provides information on the maintenance tasks that will be performed on the equipment used to manufacture the replacement parts, including the frequency and type of maintenance.

The Quality Control and Inspection module provides information on the quality control and inspection procedures used to ensure the manufactured parts meet the required specifications, including the type of inspection, parameters, and acceptance criteria.

The Human Roles module provides information on the roles of the personnel involved in the additive manufacturing process, including their responsibilities and qualifications.

The Regulations and Standards module provides information on the regulations and standards that must be met for the replacement parts to be considered safe and compliant, including the specific requirements and applicable standards.

The Safety and Environmental Considerations module provides information on the safety and environmental considerations for the replacement parts, including the potential hazards and environmental impacts.

Using the provided ontology URI <https://w3id.org/ammo/ont/>, prefix 'ammo', and the previously generated stub files for each module, please help me model the Failure Modes and Effects module by providing classes, properties, and individuals that can capture information on the potential failure modes and effects of the replacement parts. Please also provide any necessary metadata and annotations to ensure the ontology is properly documented and can be used effectively.

### ChatGPT Prompt: Quality Control and Inspection
In this session, we will be modeling the Quality Control and Inspection module of the AMMO ontology. This module provides information on the quality control and inspection procedures used to ensure the manufactured parts meet the required specifications. 

We will be working with the AMMO ontology, which can be found in the following GitHub repository: https://github.com/your-username/ammo-ontology.

Before we begin, make sure you have the latest version of the ontology pulled to your local machine and the appropriate environment set up. You can find more information on this in the README file.

For this session, we will focus on the Quality Control and Inspection module, which is defined in the `quality_control_module.ttl` file. This module should import the `common_metadata.ttl` module, which provides metadata about the ontology.

The Quality Control and Inspection module will include information about inspection procedures, including the criteria used to determine whether parts meet specifications, the tools and equipment used to perform inspections, and the personnel responsible for performing inspections. It will also include information on quality control procedures, such as statistical process control methods used to monitor the manufacturing process.

Let's begin by defining the classes, properties, and individuals needed for this module. As always, feel free to ask me any questions if you need help.

### ChatGPT Prompt: Human Roles
We are continuing to model the additive manufacturing ontology for military replacement parts. This time we will focus on the human roles involved in the process. We would like to create an ontology module that captures the roles of the personnel involved in the additive manufacturing process. The module will have to describe the different roles, the tasks performed by each role, and the equipment used by each role. Assume that we will be working with the equipment module that we previously defined. The module must be modular and use the ontology uri <https://w3id.org/ammo/ont/> and the prefix 'ammo'. We have previously created a common_metadata module that includes basic metadata about the ontology. You can assume that this has been imported into each module.

Please generate a stub for the human roles module using the template provided in the readme, and ensure that it is appropriately connected to the other modules we have defined so far.

### ChatGPT Prompt: Regulations and Standards

Hi ChatGPT, I am working on an ontology called AMMO, which stands for Additive Manufacturing for Military Operations. This ontology will model equipment, materials, processes, maintenance tasks, failure modes and effects, quality control and inspection, human roles, regulations and standards, and safety and environmental considerations.

I need your help in modeling the regulations and standards module. This module will provide information on the regulations and standards that must be met for the replacement parts to be considered safe and compliant. This could include government regulations, industry standards, or other types of guidelines.

Can you give me some prompts to start modeling this module? Please keep in mind the ontology's modular structure and the existing stubs in the GitHub repository.

Also, the prefix for the ontology is "ammo" and the ontology URI is <https://w3id.org/ammo/ont/>.

### ChatGPT Prompt: Safety and Environmental Considerations

Hi ChatGPT, I am working on the AMMO ontology, specifically the Safety and Environmental Considerations module. This module will contain information about the safety and environmental considerations that must be taken into account when manufacturing replacement parts through additive manufacturing. Some examples of considerations might include temperature and pressure limits, material handling requirements, and environmental impact. We want to ensure that the manufactured parts meet the required safety and environmental specifications, so it is important to model these considerations accurately.

To get started, could you give me some guidance on how to model this module? How can we link this module to other modules in the ontology, such as the Materials and Processes modules? And what are some example properties and classes we should define in this module to capture the necessary information about safety and environmental considerations for additive manufacturing of replacement parts?"