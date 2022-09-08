# Key Objects

[_Documentation generated by Documatic_](https://www.documatic.com)

<!---Documatic-section-visualize.visualize-start--->
## visualize.visualize

<!---Documatic-section-visualize-start--->
<!---Documatic-block-visualize.visualize-start--->
<details>
	<summary><code>visualize.visualize</code> code snippet</summary>

```python
def visualize(embed, x_test, y_test):
    feat = embed
    ax_min = np.min(embed, 0)
    ax_max = np.max(embed, 0)
    ax_dist_sq = np.sum((ax_max - ax_min) ** 2)
    plt.figure()
    ax = plt.subplot(111)
    colormap = plt.get_cmap('tab10')
    shown_images = np.array([[1.0, 1.0]])
    for i in range(feat.shape[0]):
        dist = np.sum((feat[i] - shown_images) ** 2, 1)
        if np.min(dist) < 0.0003 * ax_dist_sq:
            continue
        shown_images = np.r_[shown_images, [feat[i]]]
        patch_to_color = np.expand_dims(x_test[i], -1)
        patch_to_color = np.tile(patch_to_color, (1, 1, 3))
        patch_to_color = (1 - patch_to_color) * (1, 1, 1) + patch_to_color * colormap(y_test[i] / 10.0)[:3]
        imagebox = offsetbox.AnnotationBbox(offsetbox.OffsetImage(patch_to_color, zoom=0.5, cmap=plt.cm.gray_r), xy=feat[i], frameon=False)
        ax.add_artist(imagebox)
    plt.axis([ax_min[0], ax_max[0], ax_min[1], ax_max[1]])
    plt.title('Embedding from the last layer of the network')
    plt.show()
```
</details>
<!---Documatic-block-visualize.visualize-end--->
<!---Documatic-section-visualize-end--->

# #
<!---Documatic-section-visualize.visualize-end--->

[_Documentation generated by Documatic_](https://www.documatic.com)