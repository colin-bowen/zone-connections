%call files

filename = "SpanishPortuguese_400kV_Location_PowerGrid1";
sheetnodos = "Nodos-Localizacion";
node_name = xlsread(filename,sheetnodos,"A1:A304");
node_id = xlsread(filename, sheetnodos, "B1:B304");
node_location = xlsread(filename, sheetnodos, "C1:D304");

%columns of from and to connections
node_from = xlsread(filename, "Líneas", "B2:B440");
node_to = xlsread(filename, "Líneas", "F2:F440");

% spain nodes
ESP = xlsread(filename, "Líneas", "B2:B342");
ESP2 = xlsread(filename, "Líneas", "F2:F332");
ESP3 = xlsread(filename, "Líneas", "F338:F338");
ESP4 = xlsread(filename, "Líneas", "F341:F342");
ESP_nodes = unique([ESP;ESP2;ESP3;ESP4]);


%portugal nodes
PT1 = xlsread(filename, "Líneas", "B343:B440");
PT2 = xlsread(filename, "Líneas", "F333:F337");
PT3 = xlsread(filename, "Líneas", "F339:F340");
PT4 = xlsread(filename, "Líneas", "F343:F440");
PT_nodes = unique([PT1;PT2;PT3;PT4]);



total_nodes = unique(ESP_nodes, PT_nodes)
