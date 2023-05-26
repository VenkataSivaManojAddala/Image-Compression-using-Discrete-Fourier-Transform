% Read in image
img = imread('image.jpg');
img = double(rgb2gray(img)); % Convert to grayscale and double precision

% DFT
F = zeros(size(img));
for u = 0:size(img,1)-1
    for v = 0:size(img,2)-1
        for x = 0:size(img,1)-1
            for y = 0:size(img,2)-1
                F(u+1,v+1) = F(u+1,v+1) + img(x+1,y+1) * exp(-1i*2*pi*(u*x/size(img,1) + v*y/size(img,2)));
            end
        end
    end
end

% Compression
k = 1000; % Choose number of coefficients to keep
F(abs(F)<k) = 0; % Set small coefficients to 0

% Inverse DFT
reconstructed_img = zeros(size(img));
for x = 0:size(img,1)-1
    for y = 0:size(img,2)-1
        for u = 0:size(img,1)-1
            for v = 0:size(img,2)-1
                reconstructed_img(x+1,y+1) = reconstructed_img(x+1,y+1) + F(u+1,v+1) * exp(1i*2*pi*(u*x/size(img,1) + v*y/size(img,2)));
            end
        end
        reconstructed_img(x+1,y+1) = reconstructed_img(x+1,y+1) / (size(img,1)*size(img,2));
    end
end

% Display results
figure;
subplot(1,2,1); imshow(uint8(img)); title('Original Image');
subplot(1,2,2); imshow(uint8(abs(reconstructed_img))); title('Reconstructed Image');