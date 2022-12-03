# Created by:
# Setiadi Sulis Sandiwarno

# Import library
import pandas as pd
import plotly.express as px
import plotly.graph_objects as go


# Function to find the most occuring Label
def get_label(neighbours, y):
    zero_count, one_count = 0, 0
    for element in neighbours:
        if y[element[1]] == 0:
            zero_count += 1
        elif y[element[1]] == 1:
            one_count += 1
    if zero_count == one_count:
        return y[neighbours[0][1]]
    return 1 if one_count > zero_count else 0


# Function to calculate Euclidean Distance
def distance(element1, element2):
    x_distance = (element1[0] - element2[0]) ** 2
    y_distance = (element1[1] - element2[1]) ** 2
    return (x_distance + y_distance) ** 0.5


# Function to find the distance between input point and all points in the dataset
def find_nearest(x, y, input, k):
    distances = []
    for id, element in enumerate(x):
        distances.append([distance(input, element), id])
    distances = sorted(distances)
    predicted_label = get_label(distances[0:k], y)
    return predicted_label, distances[0:k], distances[k:]


# Create dataset
usia = [12, 14, 14, 15, 15, 16, 17, 17, 18, 18]
bb = [5.6, 5.3, 6, 8.6, 7.2, 5.4, 11, 6.5, 6.5, 5]
status_gizi = [
    'Gizi Baik',
    'Gizi Kurang',
    'Gizi Baik',
    'Gizi Lebih',
    'Gizi Baik',
    'Gizi Buruk',
    'Gizi Lebih',
    'Gizi Kurang',
    'Gizi Kurang',
    'Gizi Buruk'
]

# Create dataframe
df = pd.DataFrame(list(zip(usia, bb)), columns=['Usia', 'Berat Badan'])
df['Status Gizi'] = status_gizi

# Dataset baru untuk diprediksi
n_usia = 15
n_bb = 7

# Visualiasi dataset (Grafik akan muncul di browser)

fig = px.scatter(df, x='Usia', y='Berat Badan', symbol='Status Gizi', width=800, height=400, title='Visualiasi dataset')
fig.add_trace(go.Scatter(x=[n_usia], y=[n_bb], name="Point to Classify"))
fig.show()

# Mencari Nearest Neighbours sejumlah k = 3
x = df.to_numpy()
y = status_gizi
k = 3
input = (n_usia, n_bb)

predicted_label, nearest_neighbours, far_neighbours = find_nearest(x, y, input, k)
nearest_neighbours = [[neighbour[1], x[neighbour[1], 0], x[neighbour[1], 1], neighbour[0], y[neighbour[1]]] for
                      neighbour in nearest_neighbours]
nearest_neighbours = pd.DataFrame(nearest_neighbours, columns=['id', 'Usia', 'Berat Badan', 'Jarak', 'Status Gizi'])

# Jarak data baru dengan jumlah k = 3
print(nearest_neighbours)
print("")
print('Prediksi Status Gizi untuk data baru ' +
      '\033[4m(Usia: ' + str(n_usia) +
      ' Berat Badan: ' + str(n_bb) +
      ')\033[0m adalah: \033[1m {}'.format(predicted_label) + '\033[0m')


# Visualisasi Prediksi

# Mencari Far Neighbours
far_neighbours = [[neighbour[1], x[neighbour[1], 0], x[neighbour[1], 1], neighbour[0], y[neighbour[1]]]
                  for neighbour in far_neighbours]
far_neighbours = pd.DataFrame(far_neighbours, columns=['id', 'Usia', 'Berat Badan', 'Jarak', 'Status Gizi'])

# Visualisasi baru fig2 dengan data far neighbours
fig2 = px.scatter(far_neighbours, x='Usia', y='Berat Badan', symbol='Status Gizi',
                  symbol_map={'0': 'square-dot', '1': 'circle'}, width=800, height=400, title='Visualisasi prediksi')

# Menambahkan titik dari data baru dan nearest neighbours ke fig2
for index, neighbour in nearest_neighbours.iterrows():
    fig2.add_trace(
        go.Scatter(x=[input[0], neighbour['Usia']],
                   y=[input[1], neighbour['Berat Badan']],
                   mode='lines+markers',
                   name='id {}'.format(int(neighbour['id'])))
    )

fig2.show()
