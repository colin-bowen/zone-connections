%call files

filename = "SpanishPortuguese_400kV_Location_PowerGrid1";
sheetnodos = "Nodos-Localizacion";
node_name = xlsread(filename,sheetnodos,"A2:A305");
node_id = xlsread(filename, sheetnodos, "B2:B305");
node_location = xlsread(filename, sheetnodos, "C2:D305");

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


all_nodes = unique([ESP_nodes; PT_nodes]);

spain_center = [sum(node_location(1:235,1))/235,sum(node_location(1:235,2))/235];
port_center = [sum(node_location(236:end,1))/69,sum(node_location(236:end,2))/69];

%overall connections convert to string to make easier input into excel
connection_from = "hello";
connection_to = "hello";
for i=1:length(node_from)
    connection_from(i) = "Node_" + num2str(node_from(i));
    connection_to(i) = "Node_" + num2str(node_to(i));
end
connection_from = connection_from';
connection_to = connection_to';

%overall connections latitude and longitude
location_from = node_location(node_from,:);
location_to = node_location(node_to,:);

%create adjacency matrix for node connections
adjacency_matrix_nodes = zeros(length(node_from));
for i = 1:length(node_from))
        adjacency_matrix(node_from(i),node_to(i)) = 1;
end

%plot graph of nodes
figure
gplot(adjacency_matrix_nodes, node_location, '-.r');
