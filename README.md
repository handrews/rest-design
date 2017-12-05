```plantuml

digraph structs {
    graph [
    splines=true;
    sep="+25,25";  
    overlap=scalexy;
    nodesep=0.4;
    ]

    node [shape = point ]; start
    node [
    shape=plain 
    nodesep=.15 
    color="white" 
    margin=0 
    height=0 
    width=0
    ]

    subgraph cluster_0 {
        graph [style=invis;]

        node [
        fontsize=8 
        fontname="tahoma"
        ];

        legend [label=<
        <TABLE BORDER="0" CELLBORDER="1" CELLSPACING="0" COLOR="gray">
        <TR><TD COLSPAN="2">Legend</TD></TR>
        <TR><TD>1</TD><TD ALIGN="LEFT">exactly 1</TD></TR>
        <TR><TD>?</TD><TD ALIGN="LEFT">0 or 1</TD></TR>
        <TR><TD>*</TD><TD ALIGN="LEFT">0 or more</TD></TR>
        <TR><TD>+</TD><TD ALIGN="LEFT">1 or more</TD></TR>
        <TR><TD>(si)</TD><TD ALIGN="LEFT">safe, idempotent</TD></TR>
        <TR><TD>(ui)</TD><TD ALIGN="LEFT">unsafe, idempotent</TD></TR>
        <TR><TD>(un)</TD><TD ALIGN="LEFT">unsafe, non-idempotent</TD></TR>
        </TABLE>>];
    }

    subgraph cluster_1 {
        graph [style=invis;]

        home [label=<
        <TABLE BORDER="0" CELLBORDER="1" CELLSPACING="0" COLOR="black">
        <TR><TD bgcolor="black"><font color="white">Home</font></TD></TR>
        </TABLE>>];

        issues [label=<
        <TABLE BORDER="0" CELLBORDER="1" CELLSPACING="0" COLOR="black">
        <TR><TD bgcolor="black"><font color="white">Issues</font></TD></TR>
        </TABLE>>];

        issue [label=<
        <TABLE BORDER="0" CELLBORDER="1" CELLSPACING="0" COLOR="black">
        <TR><TD bgcolor="black"><font color="white">Issue</font></TD></TR>
        <TR><TD ALIGN="LEFT">id</TD></TR>
        <TR><TD ALIGN="LEFT">title</TD></TR>
        <TR><TD ALIGN="LEFT">(description)</TD></TR>
        <TR><TD ALIGN="LEFT">status</TD></TR>
        </TABLE>>];
    }

    start -> home
    home -> issues [label=< issues<sup>(si)</sup>>, headlabel=<<sub>1</sub>>, labelangle=35, labeldistance=1.5]

    issues:nw -> issues [label=<search<sup>(si)</sup>>, headlabel=<<sub>1</sub>>, labelangle=35, labeldistance=1.5]
    issues:ne -> issues [label=<create<sup>(un)</sup>>, headlabel=<<sub>1</sub>>, labelangle=-35, labeldistance=1.5]
    
    issues -> issue [label=< issue<sup>(si)</sup>>, headlabel=<<sub>*</sub>>, labelangle=35, labeldistance=1.5]

    issue:w -> issue [label=<open<sup>(ui)</sup>>, headlabel=<<sub>?</sub>>, labelangle=35, labeldistance=1.5]
    issue -> issue [label=<close<sup>(ui)</sup>>, headlabel=<<sub>?</sub>>, labelangle=-35, labeldistance=1.5]
    issue:s -> issue:s [label=<update<sup>(un)</sup>>, headlabel=<<sub>?</sub>>, labelangle=-35, labeldistance=1.5]
}
```