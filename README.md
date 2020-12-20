# KG-analysis



## Unification_of_Components.zip

**Description:** This component is consisted by the three smaller sub-components: (i) a Subgraph Creator which creates graphs that are used to evaluate the semantic relation of an object label with an action label or a state label, (ii) a Subgraph Similarity mechanism that evaluates if some information is worthy of entering our knowledge graph, by using the subgraphs of the previous sub-component, and (iii) Knowledge Graph Creator that inserts the knowledge in our knowledge graph, if it was found adequately important by the Subgraph Similarity sub-component


**(A) Subgraph Creator**

**Input:** The label of an Object, Action or State

**Output:** A subgraph for the Object, Action or State created from the information of ConceptNet with contextual knowledge from WordNet.

**Brief-Description:**
This sub component is executed from the DemoMain.py file which is in the directory ../Unification_of_Components/graphConstructor/DemoMain.py. As soon as the DemoMain.py is executed it will ask as input the label of an object-action-state. Then, it will start creating a subgraph from ConceptNet, based on specific ConceptNet properties. The sub-component will create a subgraph of depth 2 for each property. Sub graphs with bigger depth are to time consuming to be created. Subsequently, the sub component will add contexutal knowledge in the graph that has created, which in our case is information about household environments, based on WordNet subclasses and path patterns. The result, is a JSON file which contains a hash map as:

{InputLabel:
{N1:{property1:[node0,...,nodeN],..., propertyK:[node'0,...,node'N'], }, 
N2:{property1:{propert1:[node''0....,node''N''],...,propertyK:[node'''0,...,node'''N''']},...,propertyK:[property1:[node0'''',...,node''''N''''],...,prooertyK:[node'''''0,...,node'''''K''''']]}}}.

where InputLabel is the label which was given as input to the sub component, N1, N2 are the nodes at depth 1 and 2 respectively, property1,..., propertyK are the ConceptNet relations and nodei for i ∈ N are the nodes in ConceptNet.

**(B) Subgraph Similarity**

**Input:** Two graphs an Object-Action or Object-State

**Output:** The value of 5 different graph similarity metrics.

        (1) common nodes 
        
        (2) common paths
        
        (3) WUP similarity
        
        (4) WUP + path patterns
        
        (5) weighted sum of the four previous metrics
        
**Brief-Description:**
This sub component is executed from the graphFinal.py file which is in the directory ../Unification_of_Components/graphFinal.py. As soon as graphFinal.py is executed it will ask for the labels of an Object and an Action (or State), and a clarrification if it has to evaluate an Object-Action or an Object-State relation. Therefore, the input should be given in the form: Object Action OA (or: Object State OS). Then, the sub component will compute the values of the 5 five metrics. The final weighted metric shows to the framework if the two graph are adequately related, in order to create an object-action or object-state relation in our Knowledge Graph.

**(C) Knowlegde Ingestion**

**Input:** The label of an Object

**Output:** Json file with the actions and states that the object is adequately related.

**Brief-Description:**
This sub component is executed from the reasonerMain.py file which is in the directory ../Unification_of_Components/reasonerInfo/reasonerMain.py. This sub component expects a Json file from the vision module. Then, it evaluates if the object-action and object-state relations that the vision module found are worthy of entering our knowledge graph based on the information from the Subgraph Similarity sub component. It will then create a Json file with all the object-action and object-state relations which are adequately related, and exist in our knowledge graph.
