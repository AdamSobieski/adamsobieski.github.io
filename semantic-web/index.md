---
title: A Semantic Object Model
---

## A Semantic Object Model

Here is a sketch of a Semantic Object Model (SOM) expressed using TypeScript.

```
type IRI =
{
    readonly nodeType: 1;

    readonly namespace: string;
    readonly id: string;
}

type BlankNode =
{
    readonly nodeType: 2;

    readonly id: string;
}

type Variable =
{
    readonly nodeType: 3;

    readonly id: string;
}

type Literal =
{
    readonly nodeType: 4;

    readonly value: string;
    readonly dataType: IRI;
    readonly lang: string | null;
    readonly dir: 'ltr' | 'rtl' | null;
}

type TripleGround =
{
    readonly nodeType: 5;
    readonly isGround: true;

    /** subject */
    readonly 0: IRI | BlankNode;
    /** predicate */
    readonly 1: IRI;
    /** object */
    readonly 2: IRI | BlankNode | Literal | TripleGround;

    readonly subject: IRI | BlankNode
    readonly predicate: IRI
    readonly object: IRI | BlankNode | Literal | TripleGround;
}

type TripleNotGround =
{
    readonly nodeType: 5;
    readonly isGround: false;

    /** subject */
    readonly 0: IRI | BlankNode | Variable;
    /** predicate */
    readonly 1: IRI | Variable;
    /** object */
    readonly 2: IRI | BlankNode | Variable | Literal | Triple;

    readonly subject: IRI | BlankNode | Variable;
    readonly predicate: IRI | Variable;
    readonly object: IRI | BlankNode | Variable | Literal | Triple;
}

type Triple = | TripleGround | TripleNotGround;

type GraphGroundOnly = Iterable<TripleGround> &
{
    readonly isGroundOnly: true;
    readonly isValidOnly: boolean;
    readonly isReadOnly: boolean;

    readonly isGround: boolean;
    readonly isValid: boolean;
    readonly isEmpty: boolean;

    readonly variables: ReadonlyArray<Variable> & { readonly length: 0 };

    readonly validators: ReadonlyArray<Validator>;
    readonly provenance: Provenance | null;

    readonly baseIRI: string | null;
    readonly name: IRI | BlankNode | null;

    add(subject: IRI | BlankNode, predicate: IRI, object: IRI | BlankNode | Literal | TripleGround): boolean;
    contains(subject: IRI | BlankNode, predicate: IRI, object: IRI | BlankNode | Literal | TripleGround): boolean;
    remove(subject: IRI | BlankNode, predicate: IRI, object: IRI | BlankNode | Literal | TripleGround): boolean;
    replace(map: ReadonlyMap<Variable, IRI | BlankNode | Variable | Literal | TripleGround>, options?: GraphCreationOptions): Graph;
    update(update: Update): boolean;
}

type GraphNotGroundOnly = Iterable<Triple> &
{
    readonly isGroundOnly: false;
    readonly isValidOnly: boolean;
    readonly isReadOnly: boolean;

    readonly isGround: boolean;
    readonly isValid: boolean;
    readonly isEmpty: boolean;

    readonly variables: ReadonlyArray<Variable>;

    readonly validators: ReadonlyArray<Validator>;
    readonly provenance: Provenance | null;

    readonly baseIRI: string | null;
    readonly name: IRI | BlankNode | Variable | null;

    add(subject: IRI | BlankNode | Variable, predicate: IRI | Variable, object: IRI | BlankNode | Variable | Literal | Triple): boolean;
    contains(subject: IRI | BlankNode | Variable, predicate: IRI | Variable, object: IRI | BlankNode | Variable | Literal | Triple): boolean;
    remove(subject: IRI | BlankNode | Variable, predicate: IRI | Variable, object: IRI | BlankNode | Variable | Literal | Triple): boolean;
    replace(map: ReadonlyMap<Variable, IRI | BlankNode | Variable | Literal | Triple>, options?: GraphCreationOptions): Graph;
    update(update: Update): boolean;
}

type Graph = | GraphGroundOnly | GraphNotGroundOnly;

declare var Graph:
{
    readonly IRI: 1;
    readonly BLANK: 2;
    readonly VARIABLE: 3;
    readonly LITERAL: 4;
    readonly TRIPLE: 5;
}

class GraphCreationOptions
{
    isGroundOnly?: true | false;
    isValidOnly?: true | false;
    isReadOnly?: true | false;

    baseIRI?: string;
    name?: IRI | BlankNode | Variable;

    validators?: Iterable<Validator>;
}

type Update =
{
    readonly delete: Graph;
    readonly insert: Graph;
    readonly where: Graph;
}

type Validator = Graph &
{
    validate(graph: Graph): boolean;
    validate(graph: Graph, update: Update): boolean;
}

class ValidatorCreationOptions { }

type Reasoner = Graph &
{
    reason(source: Graph, options?: GraphCreationOptions): Graph;
}

class ReasonerCreationOptions { }

type Provenance =
{
    reasoner: Reasoner;
    source: Graph;
}

type SemanticsImplementation =
{
    createIRI(iri: string): IRI;
    createIRI(namespace: string, id: string): IRI;
    createBlank(id: string): BlankNode;
    createVariable(id: string): Variable;
    createLiteral(value: boolean | number | bigint | string, datatype?: IRI, lang?: string, dir?: 'ltr' | 'rtl'): Literal;
    createTriple(subject: IRI | BlankNode | Variable, predicate: IRI | Variable, object: IRI | BlankNode | Variable | Literal | Triple): Triple;
    createGraph(triples?: Iterable<Triple>, options?: GraphCreationOptions): Graph;
    createUpdate(deletions: Graph, insertions: Graph, where?: Graph): Update;
    createValidator(graph: Graph, options?: ValidatorCreationOptions): Validator;
    createReasoner(graph: Graph, options?: ReasonerCreationOptions): Reasoner;
}

type Semantics =
{
    readonly implementation: SemanticsImplementation;

    open(): void;

    getDescription(element: Element): GraphGroundOnly;
    hasDescription(element: Element): boolean;
    setDescription(element: Element, graph: Graph): void;
    updateDescription(element: Element, update: Update): boolean;
    deleteDescription(element: Element): void;

    close(): void;
}
```

## Usage Examples

### Example 1

```
const ex = 'http://www.example.org/ns#'
const rdf = 'http://www.w3.org/1999/02/22-rdf-syntax-ns#';
const xsd = 'http://www.w3.org/2001/XMLSchema#';

const i = window.semantics.implementation;

let graph = i.createGraph();

let widget = i.createIRI(ex, 'widget-123');
graph.add(widget, i.createIRI(rdf, 'type'), i.createIRI(ex, 'Widget'));
graph.add(widget, i.createIRI(ex, 'mass'), i.createLiteral(1234));
graph.add(widget, i.createIRI(ex, 'color'), i.createLiteral('blue'));
```

### Example 2

```
const ex = 'http://www.example.org/ns#'
const rdf = 'http://www.w3.org/1999/02/22-rdf-syntax-ns#';
const xsd = 'http://www.w3.org/2001/XMLSchema#';
const dcterms = 'http://purl.org/dc/terms/';

const i = window.semantics.implementation;

let graph = i.createGraph([], { name: i.createIRI('http://www.namedgraph.org/ns#graph-123') });

let element = window.document.getElementById('widget-123');
let component = element.id === null ? i.createBlank(nextIdentifier()) : i.createIRI(element.baseURI, element.id);

graph.add(graph.name, i.createIRI(ex, 'about'), component);
graph.add(component, i.createIRI(rdf, 'type'), i.createIRI(ex, 'Widget'));
graph.add(component, i.createIRI(ex, 'mass'), i.createLiteral(1234));
graph.add(component, i.createIRI(ex, 'color'), i.createLiteral('blue'));
graph.add(component, i.createIRI(dcterms, 'description'), i.createLiteral('...'));

window.semantics.open();
window.semantics.setDescription(element, graph);
window.semantics.close();
```

### Example 3

```
const ex = 'http://www.example.org/ns#'
const rdf = 'http://www.w3.org/1999/02/22-rdf-syntax-ns#';
const xsd = 'http://www.w3.org/2001/XMLSchema#';

const i = window.semantics.implementation;

let deletions = i.createGraph([], { isGroundOnly: false });
let insertions = i.createGraph([], { isGroundOnly: false });
let where = i.createGraph([], { isGroundOnly: false });

assert(deletions.isGroundOnly === false);
assert(insertions.isGroundOnly === false);
assert(where.isGroundOnly === false);

let x = i.createVariable('x');

deletions.add(x, i.createIRI(ex, 'color'), i.createLiteral(oldColor));
insertions.add(x, i.createIRI(ex, 'color'), i.createLiteral(newColor));
where.add(x, i.createIRI(rdf, 'type'), i.createIRI(ex, 'Widget'));
where.add(x, i.createIRI(ex, 'color'), i.createLiteral(oldColor));

let update = i.createUpdate(deletions, insertions, where);

window.semantics.open();
window.semantics.updateDescription(element, update);
window.semantics.close();
```
